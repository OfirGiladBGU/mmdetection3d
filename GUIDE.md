# Guide

## Use the docker in:
[Dockerfile](docker/Dockerfile)

## Build with:
```
docker build -t mmdet3d:latest -f docker/Dockerfile .
```

## Run with:
```
docker run -it --gpus all `
        -v ${PWD}:/workspace `
        --name mmdet3d-dev `
        mmdet3d:latest /bin/bash
```

## (Optional) Publish with:

```
docker tag mmdet3d:latest <user>/mmdet3d:latest
docker login
docker push <user>/mmdet3d:latest
```

## Check how to solve:

```
root@e84aae8414e6:/mmdetection3d# python demo/pcd_demo.py demo/data/kitti/000008.bin pointpillars_hv_secfpn_8xb6-160e_kitti-3d-car.py hv_pointpillars_secfpn_6x8_160e_kitti-3d-car_20220331_134606-d42d15ed.pth --show
12/05 22:35:40 - mmengine - WARNING - Display device not found. `--show` is forced to False
/mmdetection3d/mmdet3d/models/dense_heads/anchor3d_head.py:95: UserWarning: dir_offset and dir_limit_offset will be depressed and be incorporated into box coder in the future
  'dir_offset and dir_limit_offset will be depressed and be '
Loads checkpoint by local backend from path: hv_pointpillars_secfpn_6x8_160e_kitti-3d-car_20220331_134606-d42d15ed.pth
/opt/conda/lib/python3.7/site-packages/torch/cuda/__init__.py:106: UserWarning: 
NVIDIA GeForce RTX 5090 with CUDA capability sm_120 is not compatible with the current PyTorch installation.
The current PyTorch install supports CUDA capabilities sm_37 sm_50 sm_60 sm_61 sm_70 sm_75 sm_80 sm_86 compute_37.      
If you want to use the NVIDIA GeForce RTX 5090 GPU with PyTorch, please check the instructions at https://pytorch.org/get-started/locally/

  warnings.warn(incompatible_device_warn.format(device_name, capability, " ".join(arch_list), device_name))
12/05 22:59:15 - mmengine - WARNING - Failed to search registry with scope "mmdet3d" in the "function" registry tree. As a workaround, the current "function" registry in "mmengine" is used to build instance. This may cause unexpected failure when running the built modules. Please check whether "mmdet3d" is a correct scope, or whether the registry is initialized.
/opt/conda/lib/python3.7/site-packages/mmengine/visualization/visualizer.py:196: UserWarning: Failed to add <class 'mmengine.visualization.vis_backend.LocalVisBackend'>, please provide the `save_dir` argument.
  warnings.warn(f'Failed to add {vis_backend.__class__}, '
Inference ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Traceback (most recent call last):
  File "demo/pcd_demo.py", line 90, in <module>
    main()
  File "demo/pcd_demo.py", line 80, in main
    inferencer(**call_args)
  File "/mmdetection3d/mmdet3d/apis/inferencers/base_3d_inferencer.py", line 212, in __call__
    preds.extend(self.forward(data, **forward_kwargs))
  File "/opt/conda/lib/python3.7/site-packages/torch/autograd/grad_mode.py", line 28, in decorate_context
    return func(*args, **kwargs)
  File "/opt/conda/lib/python3.7/site-packages/mmengine/infer/infer.py", line 296, in forward
    return self.model.test_step(inputs)
  File "/opt/conda/lib/python3.7/site-packages/mmengine/model/base_model/base_model.py", line 144, in test_step
    data = self.data_preprocessor(data, False)
  File "/opt/conda/lib/python3.7/site-packages/torch/nn/modules/module.py", line 1051, in _call_impl
    return forward_call(*input, **kwargs)
  File "/mmdetection3d/mmdet3d/models/data_preprocessors/data_preprocessor.py", line 152, in forward
    return self.simple_process(data, training)
  File "/mmdetection3d/mmdet3d/models/data_preprocessors/data_preprocessor.py", line 178, in simple_process
    voxel_dict = self.voxelize(inputs['points'], data_samples)
  File "/opt/conda/lib/python3.7/site-packages/torch/autograd/grad_mode.py", line 28, in decorate_context
    return func(*args, **kwargs)
  File "/mmdetection3d/mmdet3d/models/data_preprocessors/data_preprocessor.py", line 367, in voxelize
    res_voxels, res_coors, res_num_points = self.voxel_layer(res)
  File "/opt/conda/lib/python3.7/site-packages/torch/nn/modules/module.py", line 1051, in _call_impl
    return forward_call(*input, **kwargs)
  File "/mmdetection3d/mmdet3d/models/data_preprocessors/voxelize.py", line 172, in forward
    self.deterministic)
  File "/mmdetection3d/mmdet3d/models/data_preprocessors/voxelize.py", line 89, in forward
    deterministic=deterministic)
RuntimeError: CUDA error: no kernel image is available for execution on the device
CUDA kernel errors might be asynchronously reported at some other API call,so the stacktrace below might be incorrect.  
For debugging consider passing CUDA_LAUNCH_BLOCKING=1.
```