FROM ubuntu:latest
RUN apt upgrade -y
RUN apt update -y
RUN DEBIAN_FRONTEND=noninteractive TZ="America/Bogota" apt-get -y install tzdata
RUN apt install --assume-yes software-properties-common
RUN add-apt-repository -y ppa:deadsnakes/ppa
RUN apt update -y
RUN apt install -y python3.8 python3-pip libcairo2-dev pkg-config python3-dev vim
RUN useradd -m chuky
RUN usermod -aG sudo chuky
WORKDIR /home/chuky
COPY requirements.txt /home/chuky/
COPY 11-QuickUMLS_Extraction.ipynb /home/chuky/
RUN python3 --version
RUN pip3 install --upgrade pip
RUN pip3 install numpy
RUN pip3 install Cython
RUN pip3 install pycairo
RUN pip3 install -r requirements.txt
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
EXPOSE 8888
