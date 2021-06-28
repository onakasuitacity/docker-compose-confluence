ARG CONFLUENCE_VERSION
FROM atlassian/confluence-server:${CONFLUENCE_VERSION:-latest}

ARG PROXY_NAME
RUN sed -i -e "s/\(proxyName=.*default\)('')/\1('${PROXY_NAME:-localhost}')/" /opt/atlassian/etc/server.xml.j2 \
    && sed -i -e "s/\(proxyPort=.*default\)('')/\1('80')/" /opt/atlassian/etc/server.xml.j2 \
    \
    && apt-get update -qq \
    && apt-get install -qq -y --no-install-recommends fonts-ipafont-gothic \
    && apt-get clean autoclean && apt-get autoremove -y && rm -rf /var/lib/apt/lists/* \
    && ln -s /usr/share/fonts/opentype/ipafont-gothic/ipag.ttf /opt/java/openjdk/lib/fonts/fallback/ipag.ttf \
    \
    && sed -i -e 's|export CATALINA_OPTS|CATALINA_OPTS="-Dconfluence.document.conversion.fontpath=/opt/java/openjdk/lib/fonts/fallback ${CATALINA_OPTS}"\nexport CATALINA_OPTS|g' ${CONFLUENCE_INSTALL_DIR}/bin/setenv.sh \
    && sed -i -e 's/export CATALINA_OPTS/CATALINA_OPTS="-Dconfluence.document.conversion.slides.defaultfontname.regular=IPAGothic ${CATALINA_OPTS}"\nexport CATALINA_OPTS/g' ${CONFLUENCE_INSTALL_DIR}/bin/setenv.sh \
    && sed -i -e 's/export CATALINA_OPTS/CATALINA_OPTS="-Dconfluence.document.conversion.slides.defaultfontname.asian=IPAGothic ${CATALINA_OPTS}"\nexport CATALINA_OPTS/g' ${CONFLUENCE_INSTALL_DIR}/bin/setenv.sh \
    && sed -i -e 's/export CATALINA_OPTS/CATALINA_OPTS="-Dconfluence.document.conversion.slides.defaultfontname.symbol=IPAGothic ${CATALINA_OPTS}"\nexport CATALINA_OPTS/g' ${CONFLUENCE_INSTALL_DIR}/bin/setenv.sh \
    && sed -i -e 's/export CATALINA_OPTS/CATALINA_OPTS="-Dconfluence.document.conversion.words.defaultfontname=IPAGothic ${CATALINA_OPTS}"\n\nexport CATALINA_OPTS/g' ${CONFLUENCE_INSTALL_DIR}/bin/setenv.sh