###Make sure to log into an OSC instance with GPU

Login into the virtual environment

	 source envs/my_root/bin/activate my_root

Run the imports 

    module load cuda

To run the base demo- 

    THEANO_FLAGS='device=gpu0, floatX=float32, nvcc.fastmath=True' python iGAN_main.py --model_name shoes_64
    
    source envs/my_root/bin/activate my_root
    module load cuda
    cd iGAN
    THEANO_FLAGS='device=gpu0, floatX=float32, nvcc.fastmath=True' python iGAN_main.py --model_name shoes_64


