# docker-images

See how to build each one with a readme in each folder

# Generated images
* See ghcr.io/base-band/docker-images/lattice-ci-build

# A note about how the github Actions work
* I started by trying to copy the files here https://github.com/circt/images/tree/trunk/.github/workflows but it seems like there are some secrets I need to add (The PAT) (which was needed before but seems to be not needed anymore)
* Then I half copied the work from here: https://www.cloudsavvyit.com/7138/how-to-set-up-automatic-builds-for-docker-images-on-github/
  * These instructions show you how to click through the github www and add a docker build step. This step didn't work but it DID login so I was able to work from there

