# Quick Start #

This is a quick-start guide designed to get your using epiclock with as little effort as possible. If all you want to do is display a countdown clock on your page, this is all you will need:

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
	<head>
		<title></title>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
		
		<link media="screen" rel="stylesheet" type="text/css" href="epiclock/stylesheet/jquery.epiclock.css"/>
		
		<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.4.2/jquery.min.js"></script>
		<script type="text/javascript" src="epiclock/javascript/jquery.dateformat.min.js"></script>
		<script type="text/javascript" src="epiclock/javascript/jquery.epiclock.min.js"></script>
		<script type="text/javascript">

                    //  The startup code
		    jQuery(function ()
		    {
                        jQuery('#clock').epiclock();
		    });

		</script>
	</head>
	<body>
            <div id="clock"></div>
	</body>
</html>
```

Here's a checklist of the important pieces epiclock needs to function
  1. jQuery 1.4.2+
  1. The `jquery.epiclock.min.js` script.
  1. The `jquery.epiclock.css` file.
  1. An HTML element to contain the clock (`<div id="clock"></div>`)
  1. The startup code.

# Learning More #

And that's it! That's all you need to put the default clock on a page. However, epiclock offers more than just the standard current time clock. There are a number of different [clock modes](ClockModes.md) and configuration options which can be passed to epiclock to customize it for your needs. Those are covered in the [Clock Guide](ClockGuide.md).

The epiclock library also has an extensible mechanism for defining custom renderers for displaying the clock. (Not just formatting, but altering the actual output.) This can be used for creating image clocks, passing the dates to a webservice over ajax, etc. An overview of building your own renderer is available in the [Rendering Guide](Rendering.md).

Additionally, you can customize the output format of any clock in the system using a date formatting string. The available codes, and their use, ar available in the [Date Formatting Guide](DateFormatting.md).

There's also documentation available for the [Clock Manager](ClockManager.md), which universally controls any clocks created on a page.

# Built In Demo #

The epiclock library which you download from this site includes an "index.html" file, which demonstrates some default settings for all the available clock modes.