pkg-licenses
=============
배포한 ISO 이미지에 포함된 모든 패키지의 라이선스 목록을 보여주는 도구
Upstream : https://github.com/daald/dpkg-licenses

데비안의 거의 모든 패키지는 /usr/share/doc/<packagename>/copyright 에서 저작권을 포함하고 있습니다.
하지만 이 파일은 처음에는 형식도 지정되지 않은 일반 텍스트 파일 그 안에 내용이 있는 형식이며 기계에서 읽을 수 있는 형식(http://dep.debian.net/deps/dep5/))으로 바꾸려고 시도해지만 이 내용은 필수 패키징 요구사항이 아니며, 많은 개발자들은 상관하지 않고 있습니다.

그래서 모든 패키지의 라이선스를 읽는 것은 여전히 문제이며 사업에서는 라이선스 정보에 대한 필요성이 계속 존재합니다.

http://askubuntu.com/questions/247757/how-do-you-find-the-licenses-for-everything-installed-on-your-system/620069#620069
http://stackoverflow.com/questions/1884753/license-info-of-a-deb-package#1884785

이 프로젝트는 이러한 비정형적인 파일에서 라이선스 정보를 읽으려고 노력하는 프로젝트입니다.

엑셀파일로 저장
-------------
    $ ./pkg-licenses -c > license.csv

텍스트파일로 저장
-------------
    $ ./pkg-licenses > license.csv    

실행 결과 예시
-------------

    $ ./dpkg-licenses
    St  Name             Version               Arch   Description                                   Licenses
    --  ----             -------               ----   -----------                                   --------
    ii  accountsservice  0.6.35-0ubuntu7.2     amd64  query and manipulate user account informatio  GPL-2+ GPL-3+
    ii  acl              2.2.52-1              amd64  Access control list utilities                 GPL LGPL-2.1
    ii  acpi-support     0.142                 amd64  scripts for handling many ACPI events         GPL-2+
    ii  acpid            1:2.0.21-1ubuntu2     amd64  Advanced Configuration and Power Interface e  GPL-2
    ii  adduser          3.113+nmu3ubuntu3     all    add and remove users and groups               GPL-2
    ii  alsa-base        1.0.25+dfsg-0ubuntu4  all    ALSA driver configuration files               GPL-2
    ii  alsa-utils       1.0.27.2-1ubuntu2     amd64  Utilities for configuring and using ALSA      GPL-2
    ii  anacron          2.3-20ubuntu1         amd64  cron-like program that doesn't go by time     GPL-2




설치된 패키지의 90% 정도의 라이선스 정보 검출이 가능하지만 아직 완벽하지 않습니다.

The output quality on an average workspace Ubuntu installation looks like this

    $ ./dpkg-licenses >output.txt 2>errors.txt
    $ cat output.txt | cut -c135- | wc -l
    2230
    $ cat output.txt | cut -c135- | grep unknown | wc -l
    228

Interpretation:
 2230 installed packages, success rate of tool is 1−(228/2230) = 90%

However, there is still a lot of garbage:

    ii  autoconf          2.69-6                      all    automatic configure script builder                   GFDL-1.3+ GPL-2+ GPL-2+ with Autoconf exception GPL-3+ GPL-3+ with Autoconf exception GPL-3+ with Texinfo exception MIT-X-Consortium no-modification other permissive permissive-long-disclaimer permissive-short-disclaimer permissive-without-disclaimer permissive-without-notices-or-disclaimer
    ii  bc                1.06.95-8ubuntu1            amd64  GNU bc arbitrary precision calculator language       GPL-2.0+ GPL-2.0+ with Texinfo exception permissive X11 and public-domain
    ii  cron              3.0pl1-124ubuntu2           amd64  process scheduling daemon                            Artistic GPL-2+ ISC Paul Vixie's license Paul Vixie's license and GPL-2+ and ISC
    ii  fonts-opensymbol  2:102.6+LibO4.2.8-0ubuntu3  all    OpenSymbol TrueType font                             Apache-2.0 BSD-3-clause BSD-4-clause CDDL-1.0 CDDL-1.0 | GPPL-2 GPL GPL-1 GPL-2 GPL-2+ GPL-2 | LGPL-2.1 | MPL-1.1 LGPL LGPL-2+ LGPL2+ LGPL-2.1 LGPL-2 | Apache-2.0 LGPL-3 LGPL | Apache-2.0 MIT MIT/X MPL-1.1 MPL-1.1 | GPL-2 | LGPL-2 MPL-1.1 | GPL-3+ | LGPL-3+ MPL-1.1 | LGPL-2.1 MPL 1.1 | LGPL-2+ | GPL-2+ MPL-2.0 other PSF-2 public-domain W3C Zlib
    ii  ghostscript       9.10~dfsg-0ubuntu10.4       amd64  interpreter for the PostScript language and for PDF  AFPL AFPL~AFPL AGPL-3+ Apache-2.0 BSD-3-Clause BSD-3-Clause~Adobe Expat Expat~Ghostgum Expat~SunSoft Expat~SunSoft with SunSoft exception GAP~configure GPL GPL-2+ GPL-2+ or AFPL~AFPL GPL-2+ with Autoconf exception GPL-2+ with Libtool exception GPL-2+~you GPL-2+~you or AFPL GPL-2+~you or AFPL~AFPL GPL-3+ GPL-3+~Artifex GPL~CUPS GPL~LIPS GPL~URW GPL~URW with font exception icclib LGPL-2.1+ LGPL-2.1+ and LGPL-2.1+~program-in-file LGPL-2.1~pcl3 LGPL-2.1+~program-in-file NTP~Lucent NTP~Open NTP~WSU other PD Unicode UNKNOWN ZLIB
