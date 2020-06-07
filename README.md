# SmartQueuingSystem
Exercise project to compare solutions of queue management systems with different hardware choices.
The goal is to compare the performance of each hardware solution among CPU, GPU, VPU & FPGA. 

## Running

### Set-up

Set up paths so we can run Dev Cloud utilities :
```
%env PATH=/opt/conda/bin:/opt/spark-2.4.3-bin-hadoop2.7/bin:/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/intel_devcloud_support
import os
import sys
sys.path.insert(0, os.path.abspath('/opt/intel_devcloud_support'))
sys.path.insert(0, os.path.abspath('/opt/intel'))
```

### Running locally

Example command line :
```
python person_detect.py --model=models/FP16/person-detection-retail-0013 --device=CPU --video=resources/manufacturing.avi --queue_param=queue_param/manufacturing.npy --max_people=3 --threshold=0.5 --output_path=resources
```

### Submitting jobs to Intel Dev Cloud

Below are example command lines used to submit jobs to the Intel Dev Cloud with the queue_job.sh script.

#### CPU
```
cpu_job_id = !qsub queue_job.sh -d . -l nodes=1:tank-870:i5-6500te -F "/data/models/intel/person-detection-retail-0013/FP32/person-detection-retail-0013 CPU /data/resources/manufacturing.mp4 /data/queue_param/manufacturing.npy /output/results/manufacturing/cpu 5"
```

#### GPU
```
gpu_job_id = !qsub queue_job.sh -d . -l nodes=1:tank-870:i5-6500te:intel-hd-530 -F "/data/models/intel/person-detection-retail-0013/FP16/person-detection-retail-0013 GPU /data/resources/manufacturing.mp4 /data/queue_param/manufacturing.npy /output/results/manufacturing/gpu 5"
```

#### VPU
```
vpu_job_id = !qsub queue_job.sh -d . -l nodes=1:tank-870:i5-6500te:intel-ncs2 -F "/data/models/intel/person-detection-retail-0013/FP16/person-detection-retail-0013 MYRIAD /data/resources/manufacturing.mp4 /data/queue_param/manufacturing.npy /output/results/manufacturing/vpu 5"
```

#### FPGA
```
fpga_job_id = !qsub queue_job.sh -d . -l nodes=1:tank-870:i5-6500te:iei-mustang-f100-a10 -F "/data/models/intel/person-detection-retail-0013/FP16/person-detection-retail-0013 HETERO:FPGA,CPU /data/resources/manufacturing.mp4 /data/queue_param/manufacturing.npy /output/results/manufacturing/fpga 5"
```
