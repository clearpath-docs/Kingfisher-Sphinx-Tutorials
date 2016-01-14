Teleoperation
======================== 

Download the Teleoperaiton package here: `kingfisher_teleop <http://wiki.ros.org/kingfisher_teleop>`_

Kingfisher's roscore launches from an upstart job with the following environment:

.. code:: bash

	export ROS_IP=192.168.1.1
	export ROS_MASTER_URI=http://$ROS_IP:11311

Where 192.168.1.1 is the static IP of the onboard ethernet port. This is so that the ROS upstart is not dependent on the availability or IP of the wireless connection. If the wireless requires configuration, SSH in via a wired connection to that port, and run ``wicd-curses``.

All of this is great for the availability and reliability of the background ROS process, however, it does mean that to access the roscore over wireless, you'll need to set up a static route on your workstation:

.. code:: bash

	route add -net 192.168.1.1 netmask 255.255.255.255 gw KINGFISHER_WIRELESS_IP
	export ROS_IP=WORKSTATION_WIRELESS_IP
	export ROS_MASTER_URI=http://192.168.1.1:11311

Now it should be possible to rostopic echo topics from onboard Kingfisher. If you plug in a USB joystick, you can run our basic teleop script:

.. code:: bash

	roslaunch kingfisher_teleop joystick_teleop.launch

And, of course, you can view the camera feed using ``image_view``:

.. code:: bash

	rosrun image_view image_view image:=/camera/image_color compressed
