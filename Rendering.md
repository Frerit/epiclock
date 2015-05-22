# Introduction #

Developers can create custom rendering functions as plugins to epiclock, to allow for convenient passing around of these renderers.

The heart of this system is based on the `addRenderer` function, which has the following signature:

```
    jQuery.epiclock.addRenderer('<rendererName>', function renderingFunction(element, value), function setupFunction());
```

The three major parts of the renderer are:

  1. rendererName - Used to reference the renderer in a clock.
  1. renderingFunction - Handles what to do for each value being rendered.
  1. setupFunction - Handles whatever needs to occur for the renderer as soon as the clock HTML is generated. The 'this' context of the function is the epiclock object.

An example of a custom renderer (the **retro** renderer) is included below. This rendering function uses both a CSS file along with the rendering js definition.

# Using a Custom Renderer #

After you have defined your own custom renderer, you can set your clock to use that method as follows:

```
    jQuery('#clock-retro').epiclock({format: 'h:i:s a', renderer: 'retro'});
```

# Example Renderer #

This renderer is also included in the epiclock project in the "renderers" directory.

```
/*!
 *  Retro renderer for epiclock
 *
 *  Copyright (c) Eric Garside
 *  Dual licensed under:
 *      MIT: http://www.opensource.org/licenses/mit-license.php
 *      GPLv3: http://www.opensource.org/licenses/gpl-3.0.html
 */

"use strict";

/*global window, jQuery */

/*jslint white: true, browser: true, onevar: true, undef: true, eqeqeq: true, bitwise: true, regexp: true, strict: true, newcap: true, immed: true, maxerr: 50, indent: 4 */

(function ($) {

    //------------------------------
    //
    //  Constants
    //
    //------------------------------
    
        /**
         *  Because epiclock returns values as 2 digits in one number, we need an "inner template" to contain
         *  the actual image objects.
         */
    var innerTemplate = '<span class="epiclock-img"><span class="epiclock-animation"></span></span>';

    //------------------------------
    //
    //  Animation
    //
    //------------------------------
    
    /**
     *  Animate a given element. The animation for the retro clock has four stages:
     *      :a1 - First stage of the animation
     *      :a2 - Second stage of the animation
     *      :a3 - Third stage of the animation
     *      :s  - Static image, end of animation.
     * 
     *  @param element  The element being animated.
     */
    function animate()
    {
        var clock = this;
    
        setTimeout(function ()
        {
            $('.a1', clock.container).removeClass('a1').addClass('a2');
            
            setTimeout(function ()
            {
                $('.a2', clock.container).removeClass('a2').addClass('s');
            }, 150);
        }, 150);
    }
    
    //------------------------------
    //
    //  Setup
    //
    //------------------------------

    $.epiclock.addRenderer('retro', function (element, value)
    {
            /**
             *  Determine if this is a collection of digits, or the am/pm string, and parser
             *  the value accordingly.
             */
        var digits = value.substring(1) === 'm' ? [value] : value.split('').reverse(),
            
            /**
             *  The last value of this element.
             */
            last = element.data('epiclock-last'),
            
            /**
             *  Comparison values for the last array as compared to this one.
             */
            compare = last ? last.split('').reverse() : [],
            
            /**
             *  The image instances for this block. If these don't yet exist, they will be created in the digit for...each callback.
             */
            image = $.makeArray($('.epiclock-img', element)).reverse();
            
        $.each(digits, function (index, digit)
        {
            /**
             *  We don't want to change the image part if it hasn't been updated.
             */
            if (digit === compare[index])
            {
                return;
            }
            
            /**
             *  Animate the number after the clock has changed.
             */
            $('.epiclock-animation', $(image[index] || $(innerTemplate).prependTo(element)).removeClass('d' + compare[index]).addClass('d' + digit)).removeClass('s').addClass('a1');
        });
    }, 
    
    function ()
    {
        this.bind('rendered', animate);
    });
    
}(jQuery));

```