Current hardware:  
  - Raspberry Pi 4 model B
  - Pi Cam 2.1

Maximum processed capture rate:
  - 960 x 720 px
  - 30 fps

Camera can dump an impressive amount of data into RAM.  Processing capability is less impressive.  More investigation is required to identify the limiting factor.  (RAM capacity, RAM speed, CPU used by motion, CPU used by dmcrypt, bus speed, storage write speed, etc.)

I am curious what the number value for noise_level actually means.  I have to grope for the right value.

Cloud movements:  A noise_level value of 128 ignores cloud movement, but filters out a lot of solid object movement, too.  A noise_level value of 96 seems to be more balanced, but still catches a lot of cloud movement.  Movement duration of cloud events seems to often be less than half a second.

Event duration:  I have had some success tuning the parameters to start an event, but once an event starts, it tends to go on too long (or forever).  I suspect that the parameters to start an event are not all honored when deciding whether to continue an event.

Rotation:  There should probably be a rotation schedule to clean up old videos.

Camera failure:  Sometimes I see this in the log, surrounded by a lot of non-error messages, and the camera becomes unusable until reboot:

<pre>
[1:ml1] [ERR] [VID] [Aug 25 14:00:30] v4l2_do_set_pix_format: Error setting pixel format.
VIDIOC_S_FMT: : Device or resource busy
[1:ml1] [ERR] [VID] [Aug 25 14:00:30] v4l2_set_pix_format: Palette selection failed for format UYVY: Device or resource busy
[1:ml1] [ERR] [VID] [Aug 25 14:00:30] v4l2_set_pix_format: Unable to find a compatible palette format.
[1:ml1] [ERR] [ALL] [Aug 25 14:00:30] mlp_capture: Video device fatal error - Closing video device
</pre>
