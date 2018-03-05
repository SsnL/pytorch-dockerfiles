ARG UBUNTU_VERSION
ARG CUDA_VERSION
ARG CUDNN_VERSION

FROM nvidia/cuda:${CUDA_VERSION}-cudnn${CUDNN_VERSION}-devel-ubuntu${UBUNTU_VERSION}

ENV DEBIAN_FRONTEND noninteractive

# Install common dependencies (so that this step can be cached separately)
ADD ./common/install_base.sh install_base.sh
RUN bash ./install_base.sh && rm install_base.sh

# Install Python stuff
# TODO: This looks unnecessary if we install Conda
ADD ./common/install_python.sh install_python.sh
RUN bash ./install_python.sh && rm install_python.sh

# Install user
ADD ./common/install_user.sh install_user.sh
RUN bash ./install_user.sh && rm install_user.sh

# Install conda
ARG ANACONDA_VERSION
ADD ./common/install_conda.sh install_conda.sh
RUN bash ./install_conda.sh && rm install_conda.sh

# Include BUILD_ENVIRONMENT environment variable in image
ARG BUILD_ENVIRONMENT
ENV BUILD_ENVIRONMENT ${BUILD_ENVIRONMENT}

CMD ["bash"]