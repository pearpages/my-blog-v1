---
layout: post
title:  "About printing HTML"
date:   2015-05-22 19:00:23
categories: html printing
---

There are several ways of printing a rendered html page. The easiest way, I guess is to have a specific *.css* file for the print version.

Sometimes things are not that easy, and we might to alter some of the already rendered html for whatever reason. This, might make us use some javascript.

Here comes one way of dealing with this process through javascript.

{% highlight javascript %}
/**
 * utilities to print the page
 * - Print.print(jquerySelector) or Print.print() for the full page
 * 
 * @author ppages
 * @type abstract class
 */
var Print = {
        printing: false,
        parse: function (string) {

                if ($.isPlainObject(string))
                        return string;

                var start = string.indexOf("{"), options = {};

                if (start != -1) {
                        try {
                                options = (new Function("", "var json = " + string.substr(start) + "; return JSON.parse(JSON.stringify(json));"))();
                        } catch (e) {
                        }
                }

                return options;
        },
        showTabs: function (html) {
                $('ul.uk-tab', html).each(function (i, e) {
                        var tabs = e;
                        var actualInfoId = Print.parse($(e).data('uk-tab')).connect;
                        var actualInfo = $('ul' + actualInfoId, html);

                        $('> li', actualInfo).each(function (i, e) {
                                if ($(e).html().trim() === "") {
                                        //nothing
                                } else {
                                        var tabContent = $('li', tabs).eq(i);
                                        if (tabContent.hasClass('uk-disabled')) {
                                                //nothing
                                        } else {
                                                var showTab = false;
                                                if (actualInfoId === '#listedsubsidiaries') {
                                                        if ($('> li:eq(' + i + ')', tabs).hasClass('ui-display-none')) {
                                                                //nothing
                                                        } else {
                                                                showTab = true;
                                                        }
                                                } else {
                                                        showTab = true;
                                                }

                                                if (showTab) {
                                                        var title = $('> li a', tabs).eq(i).text();

                                                        $(e).addClass('uk-active').prepend("<br/><h3>" + title + "</h3>");
                                                        if (i !== 0) {
                                                                $(e).addClass('uk-active').prepend('<br/>');
                                                        }
                                                }

                                        }
                                }


                        });
                        $(e).remove();
                });

                return html;
        },
        updateInputs: function (html) {
                var spanClass = 'form-value'

                $('ul#toasts', html).remove();

                $('p[ifyespleaseprovidedetails]', html).remove();

                //search for text inputs
                $('input:not([type=radio], [type=checkbox], [type=submit], .simple_custom_import, [type=hidden])', html).each(function (i, e) {
                        $(e).replaceWith('<span class="' + spanClass + '">' + $(e).val() + '</span>');
                });
                //remove fake inputs
                $('input[fake]', html).remove();
                $('input.fake', html).remove();


                //search for text inputs
                /*
                 $('input[type="radio"]').each(function (i, e) {
                 var name = $(e).attr('name');
                 if ($('input[type="radio"][name="' + name + '"]:checked', html).length === 0) {
                 $('input[type="radio"][name="' + name + '"]', html).eq(0).closest('label').replaceWith('<span class="' + spanClass + '">Not filled</span>');
                 $('input[type="radio"][name="' + name + '"]:not(:checked)', html).each(function (i, e) {
                 $(e).closest('label').remove();
                 });
                 } else {
                 $('input[type="radio"][name="' + name + '"]:checked', html).each(function (i, e) {
                 $(e).closest('label').replaceWith('<span class="' + spanClass + '">' + $(e).closest('label').text() + '</span>');
                 });
                 $('input[type="radio"][name="' + name + '"]:not(:checked)', html).each(function (i, e) {
                 $(e).closest('label').remove();
                 });
                 }
                 });
                 */

                //textarea
                $('textarea', html).each(function (i, e) {
                        var name = $(e).attr('name');
                        var val = $('textarea[name="' + name + '"]').val();
                        $(e).replaceWith('<div class="textarea">' + val + '</div>').css('border', '1px solid red');
                });

                //remove editors
                $('div.cke', html).remove();
                $('.fake-wysiwyg', html).remove();

                //search for all the selects
                $('select', html).each(function (i, e) {
                        $(e).replaceWith('<span class="' + spanClass + '">' + $('option:selected', e).text() + '</span>');
                });

                $('a.button', html).closest('tr').remove();

                //show tabs
                this.showTabs(html);

                return $(html).html();
        },
        updateClonedValuesForRadiosAndCheckboxes: function (html) {

                $('input:checkbox:checked,input:radio:checked').each(function (i, e) {
                        var name = $(e).attr('name');
                        var val = $(e).val();

                        $('[name="' + name + '"][value="' + val + '"]', html).prop('checked', true);
                });
        },
        linksLocalhost: function () {
                var server = document.location.hostname;
                var pre = '';
                
                var links = '';
                links += '<link href="http://' + pre + 'media/1.1/css/feb2014/font-awesome.css?' + Math.random() + '" media="screen" rel="stylesheet" type="text/css">';

                links += '<link href="http://' + pre + 'media/1.1/css/feb2014/font-awesome.css?' + Math.random() + '" media="print" rel="stylesheet" type="text/css">';
                return links;
        },
        print: function (selector, callback) {
                if (Print.printing)
                        return;

                console.log('Print.print');
                console.log(selector);

                if (typeof $_EXTRAS !== "undefined") {
                        if (typeof $_EXTRAS.worksheetTitleBarInfo !== "undefined") {

                                var windowHtml = '';
                                windowHtml += '<html><head><base href="' + $('head base').attr('href') + '"><title>' + $('#title').text() + '</title>';

                                windowHtml += Print.linksLocalhost();
                                windowHtml += '</head><body>';
                                windowHtml += '<div id="page">';
                                windowHtml += $('section[contains="fixed-title"]').clone().html();
                                windowHtml += Print.updateInputs($('div#wkt-sections').clone());
                                windowHtml += '</div>';
                                windowHtml += '<script>setTimeout(function(){window.print();},5000);</script>';
                                windowHtml += '</body></html>';

                                var mywindow = window.open('', 'Print dialog');
                                mywindow.document.write(windowHtml);
                                mywindow.document.close();
                                this.updateClonedValuesForRadiosAndCheckboxes(mywindow.document);

                                Print.printing = false;
                        }
                } else {

                        var mywindow = window.open('', 'Print dialog');
                        mywindow.document.write('<html><head><base href="' + $('head base').attr('href') + '"><title>' + $('#title').text() + '</title>');

                        var links = '';
                        var result = $('link[media="print"]');

                        $.each(result, function (index, value) {
                                links = links + "<link href='" + $(this).attr('href') + "' media='print' rel='stylesheet' type='text/css' />" +
                                        "<link href='" + $(this).attr('href') + "' media='screen' rel='stylesheet' type='text/css' />";
                        });

                        if (links) {
                                mywindow.document.write(links);
                        }

                        var html = '';
                        var inputs

                        $(':input').each(function () {
                                $(this).attr('value', $(this).val());
                        });

                        $(selector).each(function () {
                                var $clone = $(this).clone(true);
                                $clone.show();
                                $clone.removeClass('ui-display-none');

                                html += $clone.prop('outerHTML');
                        });


                        // transform html
                        $(html).find('.hasCkeditor').each(function () {
                                var data = CKEDITOR.instances[$(this).attr('id')].getData();
                                //$(this).show()
                                // $(this).autoGrow()
                                $(this).data('originalText', data);
                                // var text = $(data.replace('<br/>', "\r\n").replace('<br>', "\r\n")).text();
                                $(this).html(data);
                                $(this).css({'visibility': 'visible'});
                                var div = $('<div class="hasfulltextforprinting"></div>');
                                div.html(data);
                                $(this).after(div);
                        });
                        $(html).find('.cke').hide();

                        $(html).find('.ui-text-cut').each(function () {
                                $(this).attr('cut-text', $(this).html());
                                $(this).html($(this).attr('title'));
                        });

                        mywindow.document.write('</head><body><div id="page">');
                        mywindow.document.write(html);
                        mywindow.document.write('</div></body></html>');
                        mywindow.document.close();

                        mywindow.print();

                        Print.printing = false;
                }
                return;

        },
        init: function () {
                $.fn.printSelection = Print.print;
        }
};
$(document).ready(function () {
        Print.init();
});

{% endhighlight %}


