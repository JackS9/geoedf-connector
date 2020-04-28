BootStrap: docker
From: continuumio/miniconda3

%setup
    git clone https://github.com/JackS9/geoedf-connector.git /tmp/geoedf-connector

%environment
    export PYTHONPATH=/usr/local/lib/python3.7/dist-packages:$PYTHONPATH
    export PATH=/opt/conda/bin:/opt/conda/envs/faoinput/bin:/opt/conda/envs/datetimefilter/bin:/opt/conda/envs/nasainput/bin:/opt/conda/envs/pathfilter/bin:$PATH

%post

    apt-get update && apt-get -y install python3-pip wget curl

    cd /tmp/geoedf-connector/framework && pip3 install .

    chmod -R go+rX /usr/local/lib/python3.7/dist-packages

    cp /tmp/geoedf-connector/run-workflow-stage.sh /usr/local/bin
    chmod a+x /usr/local/bin/run-workflow-stage.sh

    chmod a+x /usr/local/bin/merge.py

    chmod a+x /usr/local/bin/collect.py

    export PATH=/opt/conda/bin:$PATH
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc

    conda create --name faoinput

    cd /tmp/geoedf-connector/faoinput && conda install -n faoinput pip && conda run -n faoinput /opt/conda/envs/faoinput/bin/pip install .

    conda create --name datetimefilter
    
    cd /tmp/geoedf-connector/datetimefilter && conda install -n datetimefilter pip && conda run -n datetimefilter /opt/conda/envs/datetimefilter/bin/pip install .

    conda create --name pathfilter
    
    cd /tmp/geoedf-connector/pathfilter && conda install -n pathfilter pip && conda run -n pathfilter /opt/conda/envs/pathfilter/bin/pip install .

    conda create --name nasainput

    cd /tmp/geoedf-connector/nasainput && conda install -n nasainput pip && conda run -n nasainput /opt/conda/envs/nasainput/bin/pip install .
