# calibrate
python txt2img.py \
	--plms \
	--no_grad_ckpt \
	--ddim_steps 50 \
	--seed 40 \
	--cond \
  	--wq 4 \
  	--ptq \
  	--aq 8 \
  	--outdir ./logs \
  	--cali \
  	--skip_grid \
  	--use_aq \
  	--ckpt ./stable-diffusion/models/ldm/stable-diffusion-v1/sd-v1-4.ckpt \
  	--config stable-diffusion/configs/stable-diffusion/v1-inference.yaml \
  	--data_path ../../dataset/COCO/annotations/captions_train2017.json \
    --cali_data_path ./q_pretrained/cali_data_128.pth \
  	--cali_save_path ./q_pretrained/cali_ckpt_128_w4a8.pth

# inference
python txt2img.py \
	--prompt "A white dog." \
  	--plms \
  	--no_grad_ckpt \
  	--ddim_steps 50 \
  	--seed 40 \
  	--cond \
  	--n_iter 1 \
  	--n_samples 1 \
  	--wq 4 \
  	--ptq \
  	--aq 8 \
  	--skip_grid \
  	--outdir ./logs/inference \
  	--use_aq \
  	--ckpt ./stable-diffusion/models/ldm/stable-diffusion-v1/sd-v1-4.ckpt \
  	--config stable-diffusion/configs/stable-diffusion/v1-inference.yaml \
  	--cali_ckpt ./q_pretrained/cali_ckpt.pth

