To use Modified model:
Step-1: Replace /segmentation-jdm/build/models/losses/focal*loss.py with /focal_loss.py
Step-2: Go to /segmentation-jdm/experiments/\_base*/models/fcn_r50-d8.py
Step-3: Change CrossEntropyLoss to FocalLoss on line 48 (in decode head)
Step-5: Add dilation=2 to decode_head = dict()
Step-6: Follow steps in README.md as it is
