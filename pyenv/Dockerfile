FROM archlinux:base-devel AS python-base
ARG PYTHON_VERSION=3.9.12

RUN pacman --noconfirm -Sy; \
    pacman --noconfirm -S archlinux-keyring; \
    pacman --noconfirm -S pyenv

ENV PYENV_ROOT=/pyenv

RUN pyenv install "$PYTHON_VERSION" \
    && pyenv global "$PYTHON_VERSION"

# Drop cache and linking files
RUN find /pyenv -type d -a \( -name __pycache__ -o -name test -o -name tests -o -name idle_test \) -exec rm -rf '{}' + \
    && find /pyenv -type f -name '*.a' -exec rm -rf '{}' +

FROM archlinux:base
ARG PYTHON_VERSION=3.9.12

COPY --from=python-base /pyenv /pyenv

ENV PATH="/pyenv/versions/${PYTHON_VERSION}/bin:${PATH}"
