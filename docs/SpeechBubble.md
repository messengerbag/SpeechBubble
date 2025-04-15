# SpeechBubble Module API

Sections:
- [Character extender methods](#character-extender-methods)
- [SpeechBubble static properties](#speechbubble-static-methods-and-properties)
- [SpeechBubble instance properties](#speechbubble-instance-properties)
- [TextOutlineStyle](#textoutlinestyle)
- [DrawingSurface extender method](#drawingsurface-extender-method)

## Character extender methods

These methods are how you actually use the SpeechBubble module. They allow you to display character speech in a speech bubble. The methods are designed to be replacements for the built-in AGS speech methods.

### Character.SayBubble

`void Character.SayBubble(String message, optional GUI* bubbleGui)`

Like `Character.Say()`, but using a speech bubble.

### Character.SayAtBubble

`void Character.SayAtBubble(int x, int y, String message, optional GUI* bubbleGui)`

Like `SayBubble()`, but the bubble will be positioned with the top-left corner at the given coordinates.

### Character.SayBackgroundBubble

`SpeechBubble* Character.SayBackgroundBubble(String message, optional bool animate, optional GUI* bubbleGui)`

Non-blocking speech, similar to SayBackground() - if `animate` is true, will play the speech animation.

### Character.ThinkBubble (NOT IMPLEMENTED)

`void Character.ThinkBubble(String message, optional GUI* bubbleGui)`

Like `Character.Think()`, but using this module's thought bubble.

### Character.GetHeight

`int Character.GetHeight(this Character*)`

Returns the current height of the character (pixels from the `Character.x` position to the top of their sprite).

### Character.StopBackgroundBubble

`bool Character.StopBackgroundBubble()`

Interrupt the character if they are speaking in the background (returns whether they were).

### Character.IsSpeakingBubble

`bool Character.IsSpeakingBubble(optional bool includeBackground)`

Returns whether the character is speaking in a bubble.

### Character.GetSpeechBubble

`SpeechBubble* Character.GetSpeechBubble()`

Returns the speech bubble used by the character (`null` if none).

## SpeechBubble static methods and properties

These methods allow you to configure the appearance and behavior of speech bubbles in the game.

### SpeechBubble.DefaultGui

`GUI* SpeechBubble.DefaultGui`

The GUI that will be used to display blocking bubbles if no GUI argument is passed. Default: null (use overlays)

### SpeechBubble.BackgroundColor

`int SpeechBubble.BackgroundColor`

The background color of speech bubbles (an AGS color number). Default: 15 (white)

### SpeechBubble.BackgroundSpeechTint

`int SpeechBubble.BackgroundSpeechTint`

The percentage by which speech bubble backgrounds are tinted by the speech color (0-100). Default: 0

### SpeechBubble.BackgroundTransparency

`int SpeechBubble.BackgroundTransparency`

The transparency of the speech bubble backgrounds (0-100). Default: 0

### SpeechBubble.BorderColor

`int SpeechBubble.BorderColor`

The border color of speech bubbles (an AGS color number). Default: 0 (black)

### SpeechBubble.BorderSpeechTint

`int SpeechBubble.BorderSpeechTint`

The percentage by which speech bubble borders are tinted by the speech color (0-100). Default: 0

### SpeechBubble.BorderTransparency

`int SpeechBubble.BorderTransparency`

The transparency of the speech bubble borders (0-100). Default: 0

### SpeechBubble.TextTransparency

`int SpeechBubble.TextTransparency`

The transparency of speech bubble text (0-100). Default: 0

### SpeechBubble.TextOutlineColor

`int SpeechBubble.TextOutlineColor`

The color of any outline applied to speech bubble text (an AGS color number). Default: 0 (black)

### SpeechBubble.TextOutlineSpeechTint

`int SpeechBubble.TextOutlineSpeechTint`

The percentage by which text outlines are tinted by the speech color (0–100). Default: 0

### SpeechBubble.TextOutlineWidth

`int SpeechBubble.TextOutlineWidth`

The width of the outline applied to speech bubble text. Default: 0 (none)

### SpeechBubble.TextOutlineStyle

`TextOutlineStyle SpeechBubble.TextOutlineStyle`

The style of the outline applied to speech bubble text. Default: `eTextOutlineRounded`

### SpeechBubble.MaxTextWidth

`int SpeechBubble.MaxTextWidth`

How wide a line of text can be before it wraps. Add left + right padding for total speech bubble width. If ≤ 0, use default AGS text wrapping. Default: 0

### SpeechBubble.PaddingTop

`int SpeechBubble.PaddingTop`

Pixels between the text and the top of speech bubbles. Default: 10

### SpeechBubble.PaddingBottom

`int SpeechBubble.PaddingBottom`

Pixels between the text and the bottom of speech bubbles. Default: 10

### SpeechBubble.PaddingLeft

`int SpeechBubble.PaddingLeft`

Pixels between the text and the left of speech bubbles. Default: 20

### SpeechBubble.PaddingRight

`int SpeechBubble.PaddingRight`

Pixels between the text and the right of speech bubbles. Default: 20

### SpeechBubble.HeightOverHead

`int SpeechBubble.HeightOverHead`

Pixels between the top of the character sprite and the bottom of the speech bubble tail (can be negative).  Default: 0

### SpeechBubble.CornerRoundingRadius

`int SpeechBubble.CornerRoundingRadius`

How many pixels to round the corners of the speech bubble by. Default: 8

### SpeechBubble.GetTalkTail()

`String[] SpeechBubble.GetTalkTail()`

Get the speech bubble "tail" to use for talk bubbles ("Say" functions), as a String "pixel array".
(See [SpeechBubble.SetTalkTail](#speechbubblesettalktail))

### SpeechBubble.SetTalkTail

`void SpeechBubble.TalkTail(String tail[])`

Set the speech bubble "tail" to use for talk bubbles ("Say" functions), as a String "pixel array".

A String pixel array is an array of strings, all of the same length, where each character represents a pixel. This allows you to draw the tail by editing the script. Use 'O' for background color, 'X' for border color and ' ' (space) for transparent. **The array must be null-terminated!**

The default array looks like this:

| **Array index** | **Content**  |
|-----------------|--------------|
| 0               | `"OOOOOOOO"` |
| 1               | `"XOOOOOXX"` |
| 2               | `"XOOOOX  "` |
| 3               | `"XOOOOX  "` |
| 4               | `" XOOOX  "` |
| 5               | `" XOOOX  "` |
| 6               | `"  XOOOX "` |
| 7               | `"   XOOOX"` |
| 8               | `"    XXX "` |
| 9               | `null`       |

Note that the top of the tail is aligned with the *inside* of the bubble border.

Example of how to use:

```
  String tail[] = new String[7];
  tail[0] = "OOOOOOOOO";
  tail[1] = "XOOOOOOOX";
  tail[2] = " XOOOOOX ";
  tail[3] = "  XOOOX  ";
  tail[4] = "   XOX   ";
  tail[5] = "    X    ";
  tail[6] = null;
  SpeechBubble.SetTalkTail(tail);
```

### SpeechBubble.TalkTailWidth

`readonly int SpeechBubble.TalkTailWidth`

Get the width of the speech bubble tail for talk bubbles.

### SpeechBubble.TalkTailHeight

`readonly int SpeechBubble.TalkTailHeight`

Get the height of the speech bubble tail for talk bubbles.

### SpeechBubble.GetThinkTail

`String[] SpeechBubble.GetThinkTail()`

Get the speech bubble "tail" to use for thought bubbles ("Think" function), as a String "pixel array".

### SpeechBubble.SetThinkTail

`void SpeechBubble.SetThinkTail(String tail[])`

Set The speech bubble "tail" to use for thought bubbles ("Think" function), as a String "pixel array".

The default array looks like this:

| **Array index** | **Content**  |
|-----------------|--------------|
| 0               | `"XXXXXXXX"` |
| 1               | `"        "` |
| 2               | `"  XX    "` |
| 3               | `" XOOX   "` |
| 4               | `"XOOOOX  "` |
| 5               | `"XOOOOX  "` |
| 6               | `" XOOX   "` |
| 7               | `"  XX    "` |
| 8               | `"        "` |
| 9               | `"    XX  "` |
| 10              | `"   XOOX "` |
| 11              | `"    XX  "` |
| 12              | `null`       |

(See [SpeechBubble.SetTalkTail](#speechbubblesettalktail))

### SpeechBubble.ThinkTailWidth

`readonly int SpeechBubble.ThinkTailWidth`

Get the width of the speech bubble tail for think bubbles.

### SpeechBubble.ThinkTailHeight

`readonly int SpeechBubble.ThinkTailHeight`

Get the height of the speech bubble tail for think bubbles.

### SpeechBubble.TextAlign

`Alignment SpeechBubble.TextAlign`

The text alignment in speech bubbles. Default: `eAlignCentre`

### SpeechBubble.InvisibleFont

`FontType SpeechBubble.InvisibleFont`

Set a font where all characters are invisible, to improve integration. Default: -1 (none)

## SpeechBubble instance properties

Properties that relate to a specific SpeechBubble instance. Except for .X and .Y which allow you to reposition the bubble, they are all read-only.

### SpeechBubble.OwningCharacter

`readonly Character* SpeechBubble.OwningCharacter`

Get the Character that this speech bubble belongs to.

### SpeechBubble.Valid

`readonly bool SpeechBubble.Valid`

Get whether this speech bubble is valid (not removed from screen).

### SpeechBubble.IsBackgroundSpeech

`readonly bool SpeechBubble.IsBackgroundSpeech`

Get whether this speech bubble is displaying non-blocking background speech.

### SpeechBubble.IsThinking

`readonly bool SpeechBubble.IsThinking`

Get whether this is a thought bubble.

### SpeechBubble.UsesGUI

`readonly bool SpeechBubble.UsesGUI`

Get whether this speech bubble is displayed on a GUI.

### SpeechBubble.Animating

`readonly bool SpeechBubble.Animating`

Get whether the character is being (manually) animated.

### SpeechBubble.Text

`readonly String SpeechBubble.Text`

Get the text of this speech bubble.

### SpeechBubble.BubbleSprite

`readonly DynamicSprite* SpeechBubble.BubbleSprite`

Get the rendered version of this speech bubble, as a `DynamicSprite`.

### SpeechBubble.BubbleOverlay

`readonly Overlay* SpeechBubble.BubbleOverlay`

Get the Overlay this speech bubble is rendered on (null if none).

### SpeechBubble.BubbleGUI

`readonly GUI* SpeechBubble.BubbleGUI`

Get the GUI this speech bubble is rendered on (null if none).

### SpeechBubble.TotalDuration

`readonly int SpeechBubble.TotalDuration`

Get the total number of game loops this speech bubble is displayed before it times out (-1 if no timeout).

### SpeechBubble.ElapsedDuration

`readonly int SpeechBubble.ElapsedDuration`

Get how many game loops this speech bubble has been displayed.

### SpeechBubble.X

`int SpeechBubble.X`

Get/set the X screen-coordinate of this speech bubble's top-left corner.

### SpeechBubble.Y

`int SpeechBubble.Y`

Get/set the Y screen-coordinate of this speech bubble's top-left corner.

## TextOutlineStyle

`enum TextOutlineStyle`

Defines the shape of the text outline. Can be one of:

* `eTextOutlineRounded` - A circular, rounded outline
* `eTextOutlineSquare` - A square "block" outline

## DrawingSurface extender method

This helper method is exposed in the API because it can be useful in other places.

### DrawingSurface.DrawStringWrappedOutline

`void DrawingSurface.DrawStringWrappedOutline(int x, int y, int width, TextOutlineStyle outlineStyle, FontType font,  Alignment alignment, String message, int transparency, int outlineColor, int outlineWidth)`

Draw a string with an outline. (Make sure the canvas has at least `outlineWidth` pixels on each side of the string.)
