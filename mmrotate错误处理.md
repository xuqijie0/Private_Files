* 安装mmrotate[开始你的第一步](https://mmdetection.readthedocs.io/zh_CN/latest/get_started.html) 

* 出现错误

  > * `from mmcv import Config, DictAction`   
  >
  >   > 发现openmmlab环境中既有mmcv，又有mmcv-full，先卸载mmcv（版本2.0.0）
  >   >
  >   > 参考[ImportError: cannot import name ‘DictAction‘ from ‘mmcv‘](https://blog.csdn.net/qq_36846729/article/details/126187707)   
  >
  > * 卸载后出现新的错误`cannot import name 'Config' from 'mmcv'` 
  >
  >   > Config从mmcv 2.0.0 移到mmengine
  >
  >   > 将`from mmcv import Config, DictAction` 改为`from mmengine.config import Config, DictAction` 
  >
  >   > 参考[[Cannot import name 'Config' from 'mmcv' (unknown location)](https://stackoverflow.com/questions/75988459/cannot-import-name-config-from-mmcv-unknown-location)]
  >
  > ***done***  
  
  
  
  >* 报错：DLL load failed while importing _imaging: 找不到指定的模块。
  >
  >  > 网上说是pillow的问题，将pillow从9.3.0升级到9.5.0
  >  >
  >  > 参考[[DLL load failed while importing _imaging:](https://stackoverflow.com/questions/66385979/dll-load-failed-while-importing-imaging)]
  >
  >***done*** 
  
  

* mmrotate整体架构

  > 具体可参考[旋转框目标检测mmrotate v0.3.1入门](https://blog.csdn.net/qq_41627642/article/details/125506315) 

  > 整体框架
  >
  > ![整体框架](https://raw.githubusercontent.com/zytx121/image-host/main/imgs/mmrotate-arch.png) 
  >
  >  
  >
  >  MMRotate 包括四个部分, `datasets`, `models`, `core` and `apis`.
  >
  > - `datasets` 用于数据加载和数据增强。 在这部分,我们支持了各种旋转目标检测数据集和数据增强预处理。
  > - `models` 包括模型和损失函数。
  > - `core` 为模型训练和评估提供工具。
  > - `apis` 为模型训练、测试和推理提供高级 API。

   

  > 模块设计
  >
  > ![整体图](https://raw.githubusercontent.com/zytx121/image-host/main/imgs/framework.png)



* 多卡运行出错

  > math.ceil(self.total_size / len(indices)))[:self.total_size]
  >
  > ZeroDivisionError: division by zero
  >
  > 数据集出错https://github.com/open-mmlab/mmdetection/issues/8276
