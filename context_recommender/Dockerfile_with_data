FROM mambaorg/micromamba:1.4.7

USER root
# Keep the base environment activated
ARG MAMBA_DOCKERFILE_ACTIVATE=1
RUN apt update && apt -y install git gcc g++ make

# Use micromamba to resolve conda-forge, much faster than conda
RUN micromamba install -y python=3.8.17 pip=20.0.2 rdkit=2020.09.5 -c conda-forge
RUN pip install \
    fastapi==0.95.1 \
    pillow==10.1.0 \
    protobuf==3.19.0 \
    pydantic==1.10.12 \
    rdchiral==1.1.0 \
    requests==2.31.0 \
    scikit-learn==1.0.2 \
    scipy==1.7.3 \
    tensorflow-cpu==2.7.4 \
    urllib3==1.26.16 \
    uvicorn==0.21.1

COPY . /app/context_recommender
WORKDIR /app/context_recommender

EXPOSE 9901

ENV CUDA_VISIBLE_DEVICES 10

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "9901"]
