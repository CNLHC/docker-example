FROM alpine:latest AS UNZIP
WORKDIR /dlzh 
COPY ./d2l-zh.zip  .
RUN  unzip d2l-zh.zip

FROM continuumio/miniconda3:latest
WORKDIR /dlzh
COPY --from=UNZIP /dlzh/ ./
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
RUN conda env create -f environment.yml
# tricky way to enable a conda enviroment 
RUN echo "source activate gluon" > ~/.bashrc

RUN pip install jupyterthemes
RUN mkdir -p $(jupyter --data-dir)/nbextensions
RUN git clone https://github.com/lambdalisue/jupyter-vim-binding $(jupyter --data-dir)/nbextensions/vim_binding

RUN conda install mxnet
RUN jt -t onedork -fs 95 -altp -tfs 11 -nfs 115 -cellw 88% -T
RUN jupyter nbextension enable vim_binding/vim_binding
CMD jupyter notebook --no-browser --port=20100 --ip=0.0.0.0 --NotebookApp.token='' --NotebookApp.password='' --allow-root


