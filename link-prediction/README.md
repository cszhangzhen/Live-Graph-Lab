# Temporal Link Prediction
For link prediction task, we use the source code provide by Roland due to its efficiency, which is publicly avaliable at [here](https://github.com/snap-stanford/roland).

## Execuate
We provide the `yaml` files for reproducing our experiments. All the detailed parameter settings are included in the `yaml` files. In the filename, 'lu' means `live update`, otherwise it is fix splitting; `d`, `w` and `m` represent `day snapshot`, `week snapshot` and `month snapshot`, respectively. For example, to run `TGCN` with `day snapshot` in `fix splitting`, just execuate the following command:
```
python main.py --cfg './roland_example_tgcn_d.yaml' --repeat 3
```