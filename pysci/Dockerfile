FROM continuumio/miniconda3:latest
WORKDIR /sweet

RUN echo  $'channels:\n\
  - defaults\n\
show_channel_urls: true\n\
default_channels:\n\
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main\n\
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free\n\
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r\n\
custom_channels:\n\
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud\n\
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud\n\
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud\n\
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud\n\
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud\n\
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud' > ~/.condarc

RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

COPY ./environment.yml ./
RUN conda env create -f environment.yml
# tricky way to enable a conda enviroment 
RUN echo "source activate sweet" > ~/.bashrc

RUN pip install jupyterthemes
RUN mkdir -p $(jupyter --data-dir)/nbextensions

RUN git clone https://github.com/lambdalisue/jupyter-vim-binding /jupyter-vim-binding
#COPY jupyter-vim-binding/ /jupyter-vim-binding
RUN mv /jupyter-vim-binding $(jupyter --data-dir)/nbextensions/vim_binding

RUN jupyter nbextension enable vim_binding/vim_binding

RUN jt -t onedork -fs 95 -altp -tfs 11 -nfs 115 -cellw 80% -T -vim

RUN conda init bash 

ENV PATH /opt/conda/envs/env/bin:$PATH

RUN source activate sweet && python3 -m pip install graphviz jupyterthemes

Run apt-get update && apt-get install graphviz

CMD  bash -c "source activate sweet && jupyter notebook\
     --port=20100\
     --no-browser\
     --ip=0.0.0.0\
     --NotebookApp.allow_origin='*'\
     --NotebookApp.token=''\
     --NotebookApp.password=''\
     --NotebookApp.base_url='/sdr'\
     --NotebookApp.base_project_url='/sdr'\
     --allow-root"
     

