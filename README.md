# SmartQueuingSystem
Exercise project to compare solutions of queue management systems

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

#### CPU
```
cpu_job_id = !qsub queue_job.sh -d . -l nodes=1:tank-870:i5-6500te -F "/data/models/intel/person-detection-retail-0013/FP32/person-detection-retail-0013 CPU /data/resources/manufacturing.mp4 /data/queue_param/manufacturing.npy /output/results/manufacturing/CPU 5"
```
