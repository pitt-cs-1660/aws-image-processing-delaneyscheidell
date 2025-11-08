FROM public.ecr.aws/lambda/python:3.13

# install uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

############
#
# TODO: implement the rest of the image
#
############
# work in lambda's task dir
WORKDIR /var/task

# 1) copy dependency spec
COPY pyproject.toml .

# 2) install deps into a local venv with uv
#    --no-dev: we don't need dev deps in lambda
#    --frozen: respect the lock if present
RUN uv sync --no-dev

# 3) copy your lambda code
COPY handler.py .

# 4) make python see the venv that uv created
#    uv puts it in .venv by default
ENV PYTHONPATH="/var/task/.venv/lib/python3.13/site-packages"

# 5) lambda entrypoint
CMD ["handler.greyscale_handler"]