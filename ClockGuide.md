# Introduction #

The epiclock plugin supports a number of different modes and configurations. These are passed into epiclock in the following format:

```
    jQuery('#some-element').epiclock({ /* Options */ });
```

# Available Options #

| **Option** | **Type** | **Description** |
|:-----------|:---------|:----------------|
| mode       | string   | The [clock mode](ClockModes.md) describes what type of clock should be rendered. |
| offset     | object   | An object containing offset values for displacing the computed time of the clock. |
| startpaused | boolean  | Flag which, if true, will start the clock off as paused. Default is false. |
| utc        | boolean  | Flag to determine if the clock should be set to UTC mode. Default is false. |
| gmt        | boolean  | Alias of utc    |
| render     | string   | A string representing a custom defined rendering function for displaying the clock. See the [Rendering Guide](Rendering.md) for more info.  |
| tare       | boolean  | Flag to determine if the clock should tare (reset) on pause. Default is false |
| format     | string   | A formatting string, as described in the [Date Formatting Guide](DateFormatting.md) |
| time       | datestring | A string to pass to the JS Date object. Used in some modes. |
| target     | datestring | Alias of time   |
| displayOffset | object   | An object containing offset values for displacing the years/days of a clock |

# The Clock Object #

Once the epiclock constructor has been called on an element, you can get reference to it's clock object by using the element's `data()` method.

```
    var clock = jQuery('#clock').epiclock({ /* Options */ }).data('epiclock');
```

The following is the API for the clock object.

| **Properties** | **Type** | **Description** |
|:---------------|:---------|:----------------|
| displayOffset  | object   | Tracks extra offsets for days and years for counter clocks. Unlike the offset object, displayOffset has no impact on computation, and is merely used to add untrackable date support (pre 1970) to the clock. |
| time           | Date     | Date object representing the base time used for computation in the clock. |
| format         | string   | A reference to the [Date Format](DateFormatting.md) string used to generate the clock. |
| mode           | string   | The current [Clock Mode](ClockModes.md) of the clock. Changing this will change the mode. |
| container      | `jQuery Object` | The jQuery Object representing the container div for this clock. |

| **Methods** |  **Description** |
|:------------|:-----------------|
| bind(event, listener) | Bind a [Clock Event](ClockEvent.md) listener. |
| pause()     | Pause a running clock. Does nothing to paused clocks. |
| resume()    | Resume a paused clock. Does nothing to running clocks. |
| toggle()    | Toggle the pause status of the clock. Pauses a running clock, resumes a paused clock. |
| destroy()   | Destroys the clock, to stop it from every running again during this page session. |
| restart(displacement) | Restart's the clock to the given _displacement_, in milliseconds. Used primarily to restart timers. In the case you just want to restart a timer, simply leave _displacement_ undefined. |
| print(format) | Print the current value of the clock, using a [Date Format](DateFormatting.md) string. |