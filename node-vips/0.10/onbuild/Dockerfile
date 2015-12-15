FROM node:0.10.41

# Build libvips
WORKDIR /tmp

ENV LIBVIPS_VERSION_MAJOR 8
ENV LIBVIPS_VERSION_MINOR 1
ENV LIBVIPS_VERSION_PATCH 0
ENV LIBVIPS_VERSION $LIBVIPS_VERSION_MAJOR.$LIBVIPS_VERSION_MINOR.$LIBVIPS_VERSION_PATCH

RUN \
  # Install dependencies
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
  apt-get install -y \
  automake build-essential curl \
  gobject-introspection gtk-doc-tools libglib2.0-dev libjpeg-turbo-progs \
  libpng12-dev libwebp-dev libtiff5-dev libexif-dev libxml2-dev swig libmagickwand-dev libpango1.0-dev \
  libmatio-dev libopenslide-dev && \
  
  # Build libvips
  curl -O http://www.vips.ecs.soton.ac.uk/supported/$LIBVIPS_VERSION_MAJOR.$LIBVIPS_VERSION_MINOR/vips-$LIBVIPS_VERSION.tar.gz && \
  tar zvxf vips-$LIBVIPS_VERSION.tar.gz && \
  cd vips-$LIBVIPS_VERSION && \
	./configure --disable-debug --disable-static --disable-introspection --disable-dependency-tracking --without-python --without-orc --without-fftw $1 && \
  make && \
  make install && \
  ldconfig && \

  # Clean up
  apt-get remove -y curl automake build-essential && \
  apt-get autoremove -y && \
  apt-get autoclean && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ONBUILD COPY package.json /usr/src/app/
ONBUILD RUN npm install
ONBUILD COPY . /usr/src/app

CMD [ "npm", "start" ]