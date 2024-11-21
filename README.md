# Keras-Pruning
Pruning CNN filters and Dense nodes (in LeNet5 model) just with Keras 

# Steps
## 1. Create Prunable Conv2D Class
This custom Keras layer extends the standard Conv2D layer with a filter masking mechanism. Each filter in the output layer is associated with a binary mask, allowing for selective activation of filters.
We have two additioal function for this class: 
1. mask_filter function: for set relative mask property to zero and
2. reset_mask function: for undo pruning action

Because in this class the pruned filters update through training phase and set them to non-zero value for back-propagation gradient we make a custom callback to make them zero at epoch end.

## 2. training
the training phase is just as before just using custom layers in model

## 3. Prune Model
Now we can Prune each layer separately with custom strategy
For this we use magnitude-base pruning

## 4. Fine-Tune Model
After pruning, fine-tune model for loss compensation

## 5. Slim Model
With defined function create model again from scratch and just load non-zero filters and remove others
