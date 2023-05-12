# Copyright 2020 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
FROM php:7.4-apache-buster
RUN apt update && apt -y install zip unzip git-all && \
echo 'deb http://apt.newrelic.com/debian/ newrelic non-free' | sudo tee /etc/apt/sources.list.d/newrelic.list && \
wget -O- https://download.newrelic.com/548C16BF.gpg | sudo apt-key add - && \
apt-get -y install newrelic-php5 
RUN NR_INSTALL_SILENT=1 newrelic-install install && \
sed -i -e "s/REPLACE_WITH_REAL_KEY/cd9571bdbcf2dc60bf4db62fe8f0b53ffc50NRAL/" \
  -e "s/newrelic.appname[[:space:]]=[[:space:]].*/newrelic.appname=\"guessbook - php\"/" \
  $(php -r "echo(PHP_CONFIG_FILE_SCAN_DIR);")/newrelic.ini
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

COPY . .

RUN composer update