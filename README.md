This project was bootstrapped with Vue

# brightness-and-contrast
```
The project is manipulating the pixel values directly to adjust the brightness and contrast value
```
## Preface

```
The project hasn't integrated the sass feature. Will integrate the feature to produce more concise 
code in the near future.
```

## Feature
```
Load and display an image file (png or jpg) from the filesystem (using a normal file picker dialog) by
clicking on the bottom-right hand "upload" button.

Once the image has been loaded, the horizontal brightness/contrast sliders become active.

The user can adjust the brightness and contrast of the image, in real time, by moving the slider left
or right from its centre position to decrease or increase brightness/contrast respectively. NOTE: By 
"real time" we mean as the slider is dragged, do not wait for a mouse up event to trigger the change 
in brightness or contrast, update it as the slider is dragged.
```
## Project setup
```
npm install
```

### Run the app
```
npm run serve
1. Visit localhost:8080
2. Select the Upload button at the bottom. 
3. Upload a png image from your local computer.
4. Adjust the slider bar to add effects on the image
5. Enjoy it!
```


