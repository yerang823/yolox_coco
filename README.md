# 1. setup environments
    python setup.py develop

# 2. demo test
    python tools/demo.py image -n yolox-s -c /path/to/your/yolox_s.pth --path assets/dog.jpg --conf 0.25 --nms 0.45 --tsize 640 --save_result --device [cpu/gpu]

# 3. train
    python -m yolox.tools.train -n yolox-s -d 8 -b 64 --fp16 -o [--cache]

> if custom data used, yolox/data/datasets/coco.py coco_classes.py
> at line 61,
> "COCO" -> "my data dir name"

# 4. eval
    python -m yolox.tools.eval -n  yolox-s -c ./YOLOX_outputs/yolox_s/best_ckpt.pth -b 8 -d 1 --conf 0.001 --machine_rank 1

> if get_local_rank() not operated, tools/eval.py 
> rank = get_local_rank() -> rank = 1 # number of specific gpu
> to see results, at line 191, tools/eval.py 
> print('summary = ', summary) 