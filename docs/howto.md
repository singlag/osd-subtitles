# OSD Subtitles

This utility combines OpenTX telemetry log files with [Betaflight] OSD elements and produces a subtitle file with OSD overlay similiar to the the Betaflight OSD. You can then play your flight video with subtitle OSD elements in a video player like [VLC] or import them into Youtube. Not all OSD elements are currently supported and some may display differently from Betaflight.

**If you have any issues or improvements you can raise them on the project site [osd-subtitles].**

## How to
First of all you need to have [telemetry](https://oscarliang.com/sbus-smartport-telemetry-naze32/) enabled for your craft and you need to have [logging](https://oscarliang.com/log-gps-coordinates-taranis/) enabled for your OpenTX transmitter. The best way is to have logging to be enabled on the same switch as the arm switch, that way logging starts and stops with the flight making it easier to combine the video with the subtitles. I recommend to have the log interval to be at least 1 second or lower.

## Log file
Start by selecting the OpenTX log file you want to import. Currently only FrSky and Crossfire telemetry have been tested. When a log file for a whioel day is loaded the individual flights inside the log file are split into different flight logs. This only works if the time between flights is less than 10 seconds. Select which flight you want to generate subtitles for. The name of the flight is the start date and the duration of the flight is in parenthesis in min:sec.

## CLI file
Next you can select the [CLI](https://oscarliang.com/betaflight-cli-explained/) dump file for the craft. You can get this information in the CLI by using "diff all" and then saving it to a text file. This step is not required but loading the correct CLI file will pre fill the values for the OSD elements, profile, units, position, craft name and display name, otherwise you will have to input them all individually. You can also save and load this information from a config file if you want to have a custom position config different from the CLI file.

## OSD elements
If you need you can change the profile used and positioning of the OSD elements. The X and Y values are in percentage of the video screen. So for example x=0%, y=0% would be in the upper left corner, x=50%, y=%50 would be in the middle and x=100%, y=100% would be in the lower right corner of the video. Note that for some players there are extra margins so subtitles start from the margin instead of the screen so that means the position doesn't always map correctly to screen size.

Select what OSD profile you want to use for the subtitles. Select the battery cell count of the craft if you display average battery voltage or you can use "Auto" which will try to guess the cell count, but this sometimes does not work correctly if the starting voltage in the log is less than maximum cell voltage, in that case select the correct number of cells. If you want to display "Craft name" and "Display name" you can input those in the corresponding fields.

The trim start field can be used to trim the start of the log. For example if you have the video start at 30 seconds into the flight, you would input 30000 in the trim start field to cut out 30 seconds from the start.

The trim end field can be used to trim the end of the log. For example if you want to cut the last 10 seconds of the log, you would input 10000 in the trim end field. The trim start and trim end can be combined to trim both from the start and the end.

The delay field is for adjusting the timing of the subtitles. This can be useful if the OSD information does not start at the same time as the video. Just note how long the delays is when the OSD should start to display in the video and input the delay here. For example if the OSD should start at 5 seconds into the video then input 5000.

## Subtitle format.

There is currently support for [SRT], [SSA] and [WebVTT] subtitle formats.

- "SRT" is very simple one line text with all values combined. This format does not include any positioning, but is widely supported.
- "SSA" format includes positioning and unicode icons. This format can be used for example to burn subtitles into video using [FFmpeg].
- "WebVTT" format includes positioning and unicode icons. This format is widely supported for web videos.
- "WebVTT (Youtube)" is the same as the WebVTT format but includes different positioning since Youtube doesn't implement the WebVTT standard correctly.

Click "Generate" to preview the output or click "Generate and save" to save the subtitle file to your computer.

[osd-subtitles]: https://github.com/kristjanbjarni/osd-subtitles/
[Betaflight]: https://betaflight.com/
[VLC]: https://www.videolan.org
[SRT]: https://en.wikipedia.org/wiki/SubRip
[WebVTT]: https://www.w3.org/TR/webvtt1/
[SSA]: https://en.wikipedia.org/wiki/SubStation_Alpha
[FFmpeg]: https://trac.ffmpeg.org/wiki/HowToBurnSubtitlesIntoVideo