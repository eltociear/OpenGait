# GaitLU-1M
![img](./Statistic.png)
GaitLU-1M represents the first large-scale unlabelled gait dataset. It consists of over one million walking sequences averaging 92 frames, namely over 92M silhouette images.

GaitLU-1M is extracted from public videos shot around the world, making it cover a wide range of variations, involving the capturing scenes (streets, subway and airport, etc.), individual attributes (gender, age and race, etc.), photography conditions (camera view, resolution, illumination and weather, etc.), and so on. 

This great diversity and scale offer an excellent chance to learn general gait representation in a self-supervised manner.

## Download (Coming soon)
Download the dataset from [Baidu Yun]() or [OneDrive]() and decompress the file by following command:
```shell
unzip -P password GaitLU-1M.zip | xargs -n1 tar xzvf
```
To obtain the password, you should sign the [Release Agreement](./Release_Agreement.pdf) and [Ethical Requirement](./Ethical_Requirements.pdf) and send the signed documents to the administrator(12131100@mail.sustech.edu.cn). 

Then you can get GaitLU-1M formatted as: 
```
silhouette_cut_pkl
├── 000                           # Random number
│   ├── 000                       # Random number
│   │   ├── 000                   # Random number
│   │   │   ├── 000_000_000.pkl   # Silhouette sequence
                ......
            ......
        ......
    ......
```


## Usage (Coming soon)
For the training phase, you should modify the `dataset_root` in `configs/gaitssb/pretrain.yaml` and run the following command:
```shell
CUDA_VISIBLE_DEVICES=0,1,2,3 python -m torch.distributed.launch --nproc_per_node=4 opengait/main.py --cfgs configs/gaitssb/pretrain.yaml --phase train --log_to_file
```
The officially provided pretrained checkpoint can be found [here](). 

Then you can evaluate the pretrained model on labelled gait datasets by runing: 
```shell
CUDA_VISIBLE_DEVICES=0,1,2,3 python -m torch.distributed.launch --nproc_per_node=4 opengait/main.py --cfgs ./configs/gaitssb/pretrain_test_on_gait3d.yaml --phase test --iter 150000
CUDA_VISIBLE_DEVICES=0,1,2,3 python -m torch.distributed.launch --nproc_per_node=4 opengait/main.py --cfgs ./configs/gaitssb/pretrain_test_on_grew.yaml --phase test --iter 150000
CUDA_VISIBLE_DEVICES=0,1,2,3 python -m torch.distributed.launch --nproc_per_node=4 opengait/main.py --cfgs ./configs/gaitssb/pretrain_test_on_casiab.yaml --phase test --iter 150000
CUDA_VISIBLE_DEVICES=0,1,2,3 python -m torch.distributed.launch --nproc_per_node=4 opengait/main.py --cfgs ./configs/gaitssb/pretrain_test_on_oumvlp.yaml --phase test --iter 150000
```

For the fine-tuning purpose, the configs displayed [here](../../configs/gaitssb/) may help you. 

## Citation
If you use this dataset in your research, please cite the following paper:
```
@ARTICLE{10242019,
  author={Fan, Chao and Hou, Saihui and Wang, Jilong and Huang, Yongzhen and Yu, Shiqi},
  journal={IEEE Transactions on Pattern Analysis and Machine Intelligence}, 
  title={Learning Gait Representation From Massive Unlabelled Walking Videos: A Benchmark}, 
  year={2023},
  volume={45},
  number={12},
  pages={14920-14937},
  doi={10.1109/TPAMI.2023.3312419}
}
```
If you think OpenGait is useful, please cite the following paper:
```
@misc{fan2022opengait,
      title={OpenGait: Revisiting Gait Recognition Toward Better Practicality}, 
      author={Chao Fan and Junhao Liang and Chuanfu Shen and Saihui Hou and Yongzhen Huang and Shiqi Yu},
      year={2022},
      eprint={2211.06597},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```