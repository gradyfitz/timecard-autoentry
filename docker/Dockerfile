FROM edtest

RUN pip install selenium canvasapi
RUN apt-get update -y && apt-get install -y curl
RUN curl https://github.com/SeleniumHQ/selenium/blob/trunk/common/manager/linux/selenium-manager?raw=true --output selenium-manager
RUN curl --location --remote-header-name https://github.com/SeleniumHQ/selenium/blob/trunk/common/manager/linux/selenium-manager?raw=true --output selenium-manager
RUN chmod 777 selenium-manager
RUN ./selenium-manager --browser chrome
RUN pip install webdriver-manager
RUN curl --location --remote-header-name https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb --output chrome-installer.deb
RUN apt install -y ./chrome-installer.deb