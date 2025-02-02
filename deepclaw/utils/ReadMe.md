utils

## Save single image or video
**Location**: deepclaw/utils/RecordImage.py  
 
**Description**: Collecting images form a camera, and save the image stream as video or single image.   

**usage**:   
``` 
    from deepclaw.utils.RecordImage import RecordImage
    # set camera controller
    camera_controller = Realsense(CAMERA_CFG)
    record_c = RecordImage(camera_controller)
    # save video
    record_c.saveVideo(SAVED_VIDEO_PATH, video_duration=10)
    # save image
    record_c.saveImage(SAVED_PIC_PATH)
```
CAMERA_CFG is your camera configuration.

## Auto collect image
**Location**: deepclaw/utils/ImageDataCollection.py   

**Description**: Auto collect images(color, depth, infrared). 
  
**usage**: 
```
    c1 = CAMERA_DRIVER
    test = ImageCollection([c1])
    test.run(saved_folder_path=YourSavedPath, show_flag=True)
```

the saved image folder structure is showed below:
```
    GraspingData
    ├── 20210125184650
    │   └── camera0
    │       ├── images
    │       │   ├── color
    │       │   ├── depth
    │       └─  └── infrared
```


## Background detector
**Location**: deepclaw/utils/ForegroundDetector.py  
 
**Description**: Detect objects in the background. Include image difference, color filter, MOG2, grabCut, rembg. 

**usage**:  
```
    from deepclaw.utils.ForegroundDetector.py import BackgroundDetector
    camera = Realsense(CAMERA_CFG)
    frame = camera.get_frame()
    color = frame.color_image[0]

    bd_test = BackgroundDetector()
    lower=np.array([10, 20, 0])
    upper=np.array([60, 80, 40])
    thresh = bd_test.filterColor(color, lower=lower, upper=upper, show_result=True)
    labels, labels_index, color_labels = bd_test.getConnectedDomain(thresh, show_label=True, region_area=2000)
```
## Auto label image
**Location**: deepclaw/utils/OfflineBackgroundDetector.py   

**Description**: Extract objects in the background.

**usage**: 
```
    # set ROI
    region_parameter = [200, 1120, 0, 720]
    # set object category
    obj_class = "paper"
    # create label folder
    label_path = YOUR_PATH_FOR_SAVED_LABEL_FOLDER
    if not os.path.isdir(label_path):
        os.makedirs(label_path)
    file_list = get_file_path(YOUR_IMAGE_FOLDER_PATH, 'jpg')
    file_list.sort()
    save_label(file_list, label_path, region_parameter, obj_class=obj_class, detect_algo='rembg')
```
## transfer mask to other format labels
**Location**: deepclaw/utils/label_format.py  
 
**Description**: transfer mask format to other label format(yolo, coco .ect). 

**usage**:  
```
    folder_path = './GraspingData/metal'
    ss = LabelGenerator(input_path=folder_path)
    ss.set_object_class('metal')
    ss.transfer2yolo()
```
Todo: add other data sets format.

## Record robot state
**Location**: deepclaw/utils/RecorderRobotData.py   

**Description**: Record and save robot running state.

**usage**:

## Self-supervise robot grasp collection
**Location**: deepclaw/utils/robot_grasp_collection.py   

**Description**: Collect grasping data using physical robot grasping.

**usage**:


## Transfer polygons format to picking format
**Location**: deepclaw/utils/polygons2pick.py   

**Description**: Collect grasping data using physical robot grasping.

**usage**:
