FROM ghcr.io/base-band/docker-images/verilator-4-016:latest
# Args get erased after FROM

# ARG VERILATOR_VERSION=2825940
# this was verilator_4_016 at some point, I think they redid their tags
ARG VERILATOR_VERSION=v4.016


ARG DEBIAN_FRONTEND=noninteractive

# Top 3 lines are boilerplate
# next, after the break are a list of general reqs
# next, are reqs for riscv
# next are reqs for lattice
# next are needed by final repo / code
# final 2 lines are boilerplate to cleanup

RUN free -h

RUN df -h