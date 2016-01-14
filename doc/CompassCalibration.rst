Compass Calibration
======================== 

Kingfisher's onboard IMU includes a magnetometer. For best performance, it's recommended to periodically re-calibrate the compass estimator which processes magnetometer data. To run the calibration routine, manually teleop Kingfisher into open water, >5m from ferrous objects and obstacles. Then, while connected by SSH, execute:

.. code:: bash

	rosrun kingfisher_bringup calibrate_compass

Kingfisher should rotate slowly in place for 60 seconds, recording compass data. Once complete, you will be prompted to enter the user password in order to save the new calibration into ``/etc/ros/hydro/imu_compass.yaml``. Once this is done, restart the ROS service to begin using the new calibration:

.. code:: bash

	sudo service kingfisher-core restart
	
Calibration should be performed when Kingfisher is first received, and any time the platform is transported more than 50km to a new launch site. It is also recommended to recalibrate annually as part of seasonal maintenance.