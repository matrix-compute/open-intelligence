# Open-Intelligence

Tools to process security camera (<b>any camera</b>) motion triggered images and sort seen objects (labels) in different categories. 
Inserts data into Postgresql database for further processing. Simple web page interface with statistics, images, voice.

Goal is to make this fairly easy to setup and powerful so.. say goodbye to privacy.

Note that `/libraries` folder has Python applications made by other people. 
I have needed to make small changes to them, that's why those are included here.


### Installing

I am later making installation more automatic but for now, 
here's steps to get environment running.

###### Python side
1. Download Python 3.6 ( https://www.python.org/ftp/python/3.6.0/python-3.6.0-amd64.exe ) 
2. Install dependencies `pip install -r requirements.txt`
3. Run `Setup.py` OR Download <b>YOLOv3-608</b> weights, cfg, coco.names https://pjreddie.com/darknet/yolo/
4. Extract weights, cfg and coco to `models` folder
5. Download Postgresql ( https://www.postgresql.org/ )
6. Rename `config.ini.tpl` to `config.ini` and fill details
7. Separate camera and folder names with comma just like at base config template

###### Api side
1. Go to `/api` folder and run `npm install`
2. Install Postgresql server: https://www.postgresql.org/
3. Rename `.env_tpl` to `.env` and fill details.
4. Run `node intelligence.js` or with PM2 process manager.
5. Access `localhost:4300` unless port modified at .env file. 


#### Project folder structure

    .
    ├── api                      # Api which is serving small static web page
    ├── classifiers              # Classifiers for different detectors like faces
    ├── dataset                  # Images of people to be detected
    ├── images                   # Input images to process
    ├── libraries                # Modified third party libraries
    ├── models                   # Yolo and other files
    ├── module                   # Source files
    ├── objects                  # Just objects
    ├── output                   # Analyse results, labels, detection images, ...
    ├── scripts                  # Scripts to ease things
    ├── LICENSE
    └── README.md


#### Postgresql notes

All datetime fields are inserted without timezone so that:

```
File     : 2020-01-03 08:51:43
Database : 2020-01-03 06:51:43.000000
```

Database timestamp need's to be shifted later to your local timezone. I have that +2 hours difference.


#### Openalpr notes

Got it running with following works.
Downloaded `2.3.0` release from here https://github.com/openalpr/openalpr/releases

1. Unzipped `openalpr-2.3.0-win-64bit.zip` to `/libraries` folder
2. Downloaded and unzipped `Source code(zip)`
3. Navigated to `src/bindings/python`
4. Run `python setup.py install`
5. From appeared `build/lib` moved contents to project `libraries/openalpr_64/openalpr` folder.
6. At license plate detection file imported contents with `from libraries.openalpr_64.openalpr import Alpr`

Now works without any python site-package installation.



#### Trouble shooting
Got `ImportError: DLL load failed: The specified module could not be found.` ???  
=> try `import cv2`, not working -> packages missing, vc redistributable etc?  
=> Windows Server for example requires desktop experience features installed.


#### Todo

Here's some ideas

- [x] implement usable **base** structure;
- [x] basic api for serving small static statistics/status web page 'command center';
- [x] voice intelligence support (web page can talk);
- [x] license plate recognition from normal camera images;
- [x] basic face recognition from cropped person images;
- [ ] identify car owners from license plates (user determines owners);
- [ ] identify persons from detected faces (user determines persons); 
- [ ] camera microphone access and speech to text conversion tools;
- [ ] automatically analyse microphone -> text contents -> find interests;
- [ ] possibility to train model... maybe coming;

## Authors

* **Norkator** - *Initial work* - [norkator](https://github.com/norkator)


### About license
Current license is not fully suitable. I don't allow commercial use.  
NonCommercial use only.