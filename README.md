## Predict using yolox_s weights
![optimize](https://user-images.githubusercontent.com/97432613/155053112-2bd09d12-c1bb-4ba8-904f-0d2d57dec17c.jpg)

## Predict using yolox_x weights
![optimize2](https://user-images.githubusercontent.com/97432613/155053133-7770f473-edbb-4348-8cbc-83ae84520723.jpg)



# 1. setup environments
    python setup.py develop

# 2. demo test
    python tools/demo.py image -n yolox-s -c /path/to/your/yolox_s.pth --path assets/dog.jpg --conf 0.25 --nms 0.45 --tsize 640 --save_result --device [cpu/gpu]

# 3. train
    python -m yolox.tools.train -n yolox-s -d 8 -b 64 --fp16 -o [--cache]

- if custom data used, 
1. Edit yolox/data/datasets/coco.py, at line 61,
    - "COCO" ----> "MyDataName"

2. Edit yolox/data/datasets/coco_classes.py

3. Edit yolo_base.py
    - self.num_clasees = 80 ----> self.num_clasees = "number of class"

4. Edit yolox.py
    - head = YOLOXHead(80) ----> head = YOLOXHead("number of class")


# 4. evaluation
    python -m yolox.tools.eval -n  yolox-s -c ./YOLOX_outputs/yolox_s/best_ckpt.pth -b 8 -d 1 --conf 0.001 --machine_rank 1


1. if get_local_rank() not operated, tools/eval.py 
    - rank = get_local_rank() -> rank = 1 # number of specific gpu

2. to see results, at line 191, tools/eval.py 
    - print('summary = ', summary) 