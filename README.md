# ObjRec_Patient_Mobility
Following are the steps to implement the object recognition and publish over a ZED node once the system is configured with relevant SDKs.

Open a new terminal and run `ZED_Diagnostic`

<img width="1426" height="792" alt="Screenshot from 2025-08-22 14-00-04" src="https://github.com/user-attachments/assets/796d68d9-7ca6-4362-9348-fe42f275b2d8" />

1. Click `Start` and ensure there are no errors.
2. Click on `AI Models`, and Optmise the ones relevant to Human body and few other (refer to the image)

<img width="1169" height="729" alt="Screenshot from 2025-08-22 14-01-05" src="https://github.com/user-attachments/assets/44e6d69e-02e0-49a4-8d3f-33b1959211fd" />

Open a new terminal and run the following commands, and you should see the following output 

`source ~/ros2_ws/install/local_setup.bash`

`ros2 launch zed_wrapper zed_camera.launch.py \`

  `camera_model:=zed2i \`
  
  `object_detection.od_enabled:=true \`
  
  `body_tracking.bt_enabled:=true \`
  
  `pos_tracking.pos_tracking_enabled:=true`


<img width="839" height="590" alt="Screenshot from 2025-08-22 14-02-18" src="https://github.com/user-attachments/assets/14687281-9a4f-4680-904c-3c924969855d" />

Open another terminal and run the following commands, and you should see the following output

'source ~/ros2_ws/install/local_setup.bash'

**Sanity checks**

`ros2 node list | grep zed_node`

`ros2 service list | grep -E "enable_obj_det|enable_body_trk"`

**If services exist, turn the modules on (harmless if already on)**

`ros2 service call /zed/zed_node/enable_obj_det std_srvs/srv/SetBool "{data: true}"`

`ros2 service call /zed/zed_node/enable_body_trk std_srvs/srv/SetBool "{data: true}"`

**Confirm topics appear**

`ros2 topic list | grep -E "obj_det|body_trk"`

**Print body tracking messages continuously**

`ros2 topic echo /zed/zed_node/body_trk/skeletons`

<img width="825" height="626" alt="Screenshot from 2025-08-22 14-02-57" src="https://github.com/user-attachments/assets/eee3fd82-cc01-4f54-a071-e6c15f2c7edf" />

The data will be available on the ROS node `/zed/zed_node/body_trk/skeletons`

**The data will contain:**

2D keypoints (skeleton_2d) — pixel coordinates of joints in the image frame

3D keypoints (skeleton_3d) — coordinates (X, Y, Z in meters) in the camera frame

3D Head coordinates (head_position) (X, Y, Z in meters) in the camera frame




