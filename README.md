# NeRF

Neural Radiance Fields (NeRF) is a technique used to generate complex 3D scenes given a set of 2D images. it interpolates between one point of view and another to create a complete scene using synthetic data.
There are many different versions of the technique, one of the most relevant is Nvidia’s instant Nerf, which is capable of creating very high quality images almost in real time. 

https://github.com/NVlabs/instant-ngp

## Instant-ngp

### Where does the rendering step take place?
	On function testbed.frame() 
### What algorithms do they use to infer the missing surfaces?
	On testbed_nerf.cu is declared #include <neural-graphics-primitives/marching_cubes.h>. Marching Cubes is algorithms to infer the missing surfaces

## Given any set of images, generate 3D scene with NeRF and export a point cloud

With Intel Xeon E-2224G and NVIDIA P1000 Harware running with windows 10 PRO this is the step for generate 3D scen with NeRF and export to PLY file.
This solution is base on Nerfstudio

1. Install CUDA (v12.1)
2. Install Python (v3.9)
3. Download Colmap (https://github.com/colmap/colmap/releases). And update on "Environment variables".
4. Download set of images (https://github.com/NVlabs/instant-ngp/tree/master/data/nerf/fox) 
5. Open CMD
6. install nerfstudio
```bash
>pip install nerfstudio
```
7. install torch
```bash
>pip install torch==2.1.2 torchvision==0.16.2 --index-url https://download.pytorch.org/whl/cu118
```
8. install tiny-cuda-nn
```bash
>pip install git+https://github.com/NVlabs/tiny-cuda-nn/#subdirectory=bindings/torch
```
9. Train NeRF
```bash
>ns-train nerfacto --data Path\to\images --pipeline.model.predict-normals True
```
10. Export to PLY file
```bash
 >ns-export pointcloud --load-config Path\to\images\nerfacto\"year"-"month"-"day"_"time"\config.yml --output-dir exports/ --num-points 1000000 --remove-outliers True --normal-method model_output --normal-output-name normals 
```

* images/: Contains the source images.
* results/: Contains the generated output files and screenshot.
