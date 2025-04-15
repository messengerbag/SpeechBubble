# SpeechBubble
SpeechBubble is a script module for [Adventure Game Studio (AGS)](http://www.adventuregamestudio.co.uk/). Version 0.9 requires AGS v3.6.0 or higher, while version 0.8 requires AGS v3.4.0 or higher.

This module allows you to display conversation text in comic book-style speech bubbles. The appearance of the speech bubbles can be extensively customized.

THIS MODULE IS UNFINISHED. SOME FEATURES ARE NOT YET IMPLEMENTED, AND OTHERS MAY CHANGE BEFORE THE FINAL RELEASE.

## How To Use
To use, you call `Character.SayBubble()`. For example:

```adventure-game-studio
player.SayBubble("This line will be said in a speech bubble");
```

You can also use `Character.SayAtBubble()` to position the bubble elsewhere on screen, and `Character.SayBackgroundBubble()` for non-blocking speech. `Character.ThinkBubble()` IS NOT YET IMPLEMENTED.

To configure the appearance of the speech bubbles, you set the SpeechBubble properties. This is usually best done in GlobalScript `game_start()`. For example:

```adventure-game-studio
function game_start()
{
  SpeechBubble.BorderColor = Game.GetColorFromRGB(0,128,0);
  SpeechBubble.BackgroundColor = Game.GetColorFromRGB(128,255,128);
  SpeechBubble.BackgroundTransparency = 33;
  SpeechBubble.PaddingTop = 5;
  SpeechBubble.PaddingBottom = 5;
  SpeechBubble.PaddingLeft = 15;
  SpeechBubble.PaddingRight = 15;
  // Other code
}
```

See the declaration below for the full list and explanation of the properties.

The module relies on built-in AGS settings as far as possible. In particular, it uses these settings to customize the appearance and behavior of the speech bubbles:

* `Character.SpeechColor`
* `Game.SpeechFont`
* `Game.TextReadingSpeed`
* `Speech.SkipStyle`
* `Speech.VoiceMode`

Note that to get text-based lip sync to work, you need to provide an invisible font, and set the `SpeechBubble.InvisibleFont` property accordingly. You may download one here:

  http://www.angelfire.com/pr/pgpf/if.html

Finally, the module (usually) calls `Character.Say()` to render speech animation and play voice clips. If you are already using some custom Say module (e.g. [TotalLipSync](https://github.com/messengerbag/TotalLipSync)), you may want to call a custom Say() function instead. To do this, simply change the function call in `SB_sayImpl()` at the top of SpeechBubble.asc.

## API

- [Character extender methods](docs/SpeechBubble.md#character-extender-methods)
  - [Character.SayBubble](docs/SpeechBubble.md#charactersaybubble)
  - [Character.SayAtBubble](docs/SpeechBubble.md#charactersayatbubble)
  - [Character.SayBackgroundBubble](docs/SpeechBubble.md#charactersaybackgroundbubble)
  - [Character.ThinkBubble (NOT IMPLEMENTED)](docs/SpeechBubble.md#characterthinkbubble)
  - [Character.GetHeight](docs/SpeechBubble.md#charactergetheight)
  - [Character.StopBackgroundBubble](docs/SpeechBubble.md#characterstopbackgroundbubble)
  - [Character.IsSpeakingBubble](docs/SpeechBubble.md#characterisspeakingbubble)
  - [Character.GetSpeechBubble](docs/SpeechBubble.md#charactergetspeechbubble)
- [SpeechBubble static properties](docs/SpeechBubble.md#speechbubble-static-properties)
  - [SpeechBubble.DefaultGui](docs/SpeechBubble.md#speechbubbledefaultgui)
  - [SpeechBubble.BackgroundColor](docs/SpeechBubble.md#speechbubblebackgroundcolor)
  - [SpeechBubble.BackgroundSpeechTint](docs/SpeechBubble.md#speechbubblebackgroundspeechtint)
  - [SpeechBubble.BackgroundTransparency](docs/SpeechBubble.md#speechbubblebackgroundtransparency)
  - [SpeechBubble.BorderColor](docs/SpeechBubble.md#speechbubblebordercolor)
  - [SpeechBubble.BorderSpeechTint](docs/SpeechBubble.md#speechbubbleborderspeechtint)
  - [SpeechBubble.BorderTransparency](docs/SpeechBubble.md#speechbubblebordertransparency)
  - [SpeechBubble.TextTransparency](docs/SpeechBubble.md#speechbubbletexttransparency)
  - [SpeechBubble.TextOutlineColor](docs/SpeechBubble.md#speechbubbletextoutlinecolor)
  - [SpeechBubble.TextOutlineSpeechTint](docs/SpeechBubble.md#speechbubbletextoutlinespeechtint)
  - [SpeechBubble.TextOutlineWidth](docs/SpeechBubble.md#speechbubbletextoutlinewidth)
  - [SpeechBubble.TextOutlineStyle](docs/SpeechBubble.md#speechbubbletextoutlinestyle)
  - [SpeechBubble.MaxTextWidth](docs/SpeechBubble.md#speechbubblemaxtextwidth)
  - [SpeechBubble.PaddingTop](docs/SpeechBubble.md#speechbubblepaddingtop)
  - [SpeechBubble.PaddingBottom](docs/SpeechBubble.md#speechbubblepaddingbottom)
  - [SpeechBubble.PaddingLeft](docs/SpeechBubble.md#speechbubblepaddingleft)
  - [SpeechBubble.PaddingRight](docs/SpeechBubble.md#speechbubblepaddingright)
  - [SpeechBubble.HeightOverHead](docs/SpeechBubble.md#speechbubbleheightoverhead)
  - [SpeechBubble.CornerRoundingRadius](docs/SpeechBubble.md#speechbubblecornerroundingradius)
  - [SpeechBubble.TalkTail](docs/SpeechBubble.md#speechbubbletalktail)
  - [SpeechBubble.TalkTailWidth](docs/SpeechBubble.md#speechbubbletalktailwidth)
  - [SpeechBubble.TalkTailHeight](docs/SpeechBubble.md#speechbubbletalktailheight)
  - [SpeechBubble.ThinkTail](docs/SpeechBubble.md#speechbubblethinktail)
  - [SpeechBubble.ThinkTailWidth](docs/SpeechBubble.md#speechbubblethinktailwidth)
  - [SpeechBubble.ThinkTailHeight](docs/SpeechBubble.md#speechbubblethinktailheight)
  - [SpeechBubble.TextAlign](docs/SpeechBubble.md#speechbubbletextalign)
  - [SpeechBubble.InvisibleFont](docs/SpeechBubble.md#speechbubbleinvisiblefont)
- [SpeechBubble instance properties](docs/SpeechBubble.md#speechbubble-instance-properties)
  - [SpeechBubble.OwningCharacter](docs/SpeechBubble.md#speechbubbleowningcharacter)
  - [SpeechBubble.Valid](docs/SpeechBubble.md#speechbubblevalid)
  - [SpeechBubble.IsBackgroundSpeech](docs/SpeechBubble.md#speechbubbleisbackgroundspeech)
  - [SpeechBubble.IsThinking](docs/SpeechBubble.md#speechbubbleisthinking)
  - [SpeechBubble.UsesGUI](docs/SpeechBubble.md#speechbubbleusesgui)
  - [SpeechBubble.Animating](docs/SpeechBubble.md#speechbubbleanimating)
  - [SpeechBubble.Text](docs/SpeechBubble.md#speechbubbletext)
  - [SpeechBubble.BubbleSprite](docs/SpeechBubble.md#speechbubblebubblesprite)
  - [SpeechBubble.BubbleOverlay](docs/SpeechBubble.md#speechbubblebubbleoverlay)
  - [SpeechBubble.BubbleGUI](docs/SpeechBubble.md#speechbubblebubblegui)
  - [SpeechBubble.TotalDuration](docs/SpeechBubble.md#speechbubbletotalduration)
  - [SpeechBubble.ElapsedDuration](docs/SpeechBubble.md#speechbubbleelapsedduration)
  - [SpeechBubble.X](docs/SpeechBubble.md#speechbubblex)
  - [SpeechBubble.Y](docs/SpeechBubble.md#speechbubbley)
- [TextOutlineStyle](docs/SpeechBubble.md#textoutlinestyle)
- [DrawingSurface extender method](docs/SpeechBubble.md#drawingsurface-extender-method)
  - [DrawingSurface.DrawStringWrappedOutline](docs/SpeechBubble.md#drawingsurfacedrawstringwrappedoutline)
  
## Change Log

* 0.9.0:
  * Updated to use API for AGS 3.6.0
  * Exposed `DrawingSurface.DrawStringWrappedOutline()` as an extender function
  * Updated readme and API documentation

## License details
Development of this module was funded by AGS forum member bx83, who agreed to make the code open-source. Thanks!

This code is offered under the MIT License:
  https://opensource.org/licenses/MIT

It is also licensed under a Creative Commons Attribution 4.0 International License:
  https://creativecommons.org/licenses/by/4.0/
