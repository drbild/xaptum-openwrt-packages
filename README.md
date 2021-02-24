# Xaptum feed for OpenWrt

## Description

This feed contains OpenWrt packages for Xaptum software.

## Usage

To enable this feed, add the following line to your feeds.conf:
```
src-git xaptum https://github.com/xaptum/xaptum-openwrt-packages.git
```

To install all its package definitions, run:
```
./scripts/feeds update xaptum
./scripts/feeds install -a -p xaptum
```

## License

Copyright 2021 Xaptum, Inc.

Licensed under the Apache License, Version 2.0 (the "License"); you may not
use this work except in compliance with the License. You may obtain a copy of
the License from the LICENSE.txt file or at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
License for the specific language governing permissions and limitations under
the License.
