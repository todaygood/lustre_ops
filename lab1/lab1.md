# lustre 单机实验






## 环境准备


https://download.rockylinux.org/pub/rocky/   在家访问挺快的。 

`virt-customize -a rhel7.5.beta1.qcow2 --root-password password:PASSWORD`

## lab1






[root@el9-1 yum.repos.d]# yum makecache 
e2fsprogs                                                                                               4.1 kB/s | 8.9 kB     00:02    
lustre-server                                                                                           162 kB/s | 1.5 MB     00:09    
lustre-client                                                                                            29 kB/s |  70 kB     00:02    
Rocky Linux 9 - BaseOS                                                                                  2.6 kB/s | 4.1 kB     00:01    
Rocky Linux 9 - AppStream                                                                               4.4 kB/s | 4.5 kB     00:01    
Rocky Linux 9 - AppStream                                                                               232 kB/s | 8.4 MB     00:36    
Rocky Linux 9 - Extras                                                                                  3.5 kB/s | 2.9 kB     00:00    
Metadata cache created.
[root@el9-1 yum.repos.d]# yum install e2fsprogs
Last metadata expiration check: 2:49:12 ago on Sat 10 May 2025 08:33:19 AM UTC.
Package e2fsprogs-1.46.5-5.el9.x86_64 is already installed.
Dependencies resolved.
========================================================================================================================================
 Package                            Architecture               Version                              Repository                     Size
========================================================================================================================================
Upgrading:
 e2fsprogs                          x86_64                     1.47.1-wc2.el9                       e2fsprogs                     1.0 M
 e2fsprogs-libs                     x86_64                     1.47.1-wc2.el9                       e2fsprogs                     247 k
 libcom_err                         x86_64                     1.47.1-wc2.el9                       e2fsprogs                      27 k
 libss                              x86_64                     1.47.1-wc2.el9                       e2fsprogs                      32 k

Transaction Summary
========================================================================================================================================
Upgrade  4 Packages

Total download size: 1.3 M
Is this ok [y/N]: y
Downloading Packages:
(1/4): libcom_err-1.47.1-wc2.el9.x86_64.rpm                                                              19 kB/s |  27 kB     00:01    
(2/4): libss-1.47.1-wc2.el9.x86_64.rpm                                                                   65 kB/s |  32 kB     00:00    
(3/4): e2fsprogs-libs-1.47.1-wc2.el9.x86_64.rpm                                                         126 kB/s | 247 kB     00:01    
(4/4): e2fsprogs-1.47.1-wc2.el9.x86_64.rpm                                                               81 kB/s | 1.0 MB     00:12    
----------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                   105 kB/s | 1.3 MB     00:12     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                1/1 
  Upgrading        : libcom_err-1.47.1-wc2.el9.x86_64                                                                               1/8 
  Running scriptlet: libcom_err-1.47.1-wc2.el9.x86_64                                                                               1/8 
  Upgrading        : e2fsprogs-libs-1.47.1-wc2.el9.x86_64                                                                           2/8 
  Running scriptlet: e2fsprogs-libs-1.47.1-wc2.el9.x86_64                                                                           2/8 
  Upgrading        : libss-1.47.1-wc2.el9.x86_64                                                                                    3/8 
  Running scriptlet: libss-1.47.1-wc2.el9.x86_64                                                                                    3/8 
  Upgrading        : e2fsprogs-1.47.1-wc2.el9.x86_64                                                                                4/8 
  Cleanup          : e2fsprogs-1.46.5-5.el9.x86_64                                                                                  5/8 
  Cleanup          : e2fsprogs-libs-1.46.5-5.el9.x86_64                                                                             6/8 
  Cleanup          : libss-1.46.5-5.el9.x86_64                                                                                      7/8 
  Cleanup          : libcom_err-1.46.5-5.el9.x86_64                                                                                 8/8 
  Running scriptlet: libcom_err-1.46.5-5.el9.x86_64                                                                                 8/8 
  Verifying        : e2fsprogs-1.47.1-wc2.el9.x86_64                                                                                1/8 
  Verifying        : e2fsprogs-1.46.5-5.el9.x86_64                                                                                  2/8 
  Verifying        : e2fsprogs-libs-1.47.1-wc2.el9.x86_64                                                                           3/8 
  Verifying        : e2fsprogs-libs-1.46.5-5.el9.x86_64                                                                             4/8 
  Verifying        : libcom_err-1.47.1-wc2.el9.x86_64                                                                               5/8 
  Verifying        : libcom_err-1.46.5-5.el9.x86_64                                                                                 6/8 
  Verifying        : libss-1.47.1-wc2.el9.x86_64                                                                                    7/8 
  Verifying        : libss-1.46.5-5.el9.x86_64                                                                                      8/8 

Upgraded:
  e2fsprogs-1.47.1-wc2.el9.x86_64  e2fsprogs-libs-1.47.1-wc2.el9.x86_64  libcom_err-1.47.1-wc2.el9.x86_64  libss-1.47.1-wc2.el9.x86_64 

Complete!

```bash
[root@el9-1 yum.repos.d]# yum install -y lustre
Last metadata expiration check: 2:52:05 ago on Sat 10 May 2025 08:33:19 AM UTC.
Dependencies resolved.
========================================================================================================================================
 Package                                Architecture         Version                                  Repository                   Size
========================================================================================================================================
Installing:
 kernel-core                            x86_64               5.14.0-427.31.1_lustre.el9               lustre-server                20 M
 lustre                                 x86_64               2.16.1-1.el9                             lustre-server               977 k
Upgrading:
 openssl                                x86_64               1:3.2.2-6.el9_5.1                        baseos                      1.3 M
 openssl-libs                           x86_64               1:3.2.2-6.el9_5.1                        baseos                      2.4 M
Installing dependencies:
 kernel-modules-core                    x86_64               5.14.0-427.31.1_lustre.el9               lustre-server                32 M
 kmod-lustre                            x86_64               2.16.1-1.el9                             lustre-server               5.2 M
 kmod-lustre-osd-ldiskfs                x86_64               2.16.1-1.el9                             lustre-server               738 k
 lustre-osd-ldiskfs-mount               x86_64               2.16.1-1.el9                             lustre-server                20 k
 perl-AutoLoader                        noarch               5.74-481.el9                             appstream                    20 k
 perl-B                                 x86_64               1.80-481.el9                             appstream                   178 k
 perl-Carp                              noarch               1.50-460.el9                             appstream                    29 k
 perl-Class-Struct                      noarch               0.66-481.el9                             appstream                    21 k
 perl-Data-Dumper                       x86_64               2.174-462.el9                            appstream                    55 k
 perl-Digest                            noarch               1.19-4.el9                               appstream                    25 k
 perl-Digest-MD5                        x86_64               2.58-4.el9                               appstream                    36 k
 perl-Encode                            x86_64               4:3.08-462.el9                           appstream                   1.7 M
 perl-Errno                             x86_64               1.30-481.el9                             appstream                    13 k
 perl-Exporter                          noarch               5.74-461.el9                             appstream                    31 k
 perl-Fcntl                             x86_64               1.13-481.el9                             appstream                    19 k
 perl-File-Basename                     noarch               2.85-481.el9                             appstream                    16 k
 perl-File-Path                         noarch               2.18-4.el9                               appstream                    35 k
 perl-File-Temp                         noarch               1:0.231.100-4.el9                        appstream                    59 k
 perl-File-stat                         noarch               1.09-481.el9                             appstream                    16 k
 perl-FileHandle                        noarch               2.03-481.el9                             appstream                    14 k
 perl-Getopt-Long                       noarch               1:2.52-4.el9                             appstream                    60 k
 perl-Getopt-Std                        noarch               1.12-481.el9                             appstream                    14 k
 perl-HTTP-Tiny                         noarch               0.076-462.el9                            appstream                    53 k
 perl-IO                                x86_64               1.43-481.el9                             appstream                    85 k
 perl-IO-Socket-IP                      noarch               0.41-5.el9                               appstream                    42 k
 perl-IO-Socket-SSL                     noarch               2.073-2.el9                              appstream                   214 k
 perl-IPC-Open3                         noarch               1.21-481.el9                             appstream                    21 k
 perl-MIME-Base64                       x86_64               3.16-4.el9                               appstream                    30 k
 perl-Mozilla-CA                        noarch               20200520-6.el9                           appstream                    12 k
 perl-Net-SSLeay                        x86_64               1.94-1.el9                               appstream                   391 k
 perl-POSIX                             x86_64               1.94-481.el9                             appstream                    95 k
 perl-PathTools                         x86_64               3.78-461.el9                             appstream                    85 k
 perl-Pod-Escapes                       noarch               1:1.07-460.el9                           appstream                    20 k
 perl-Pod-Perldoc                       noarch               3.28.01-461.el9                          appstream                    83 k
 perl-Pod-Simple                        noarch               1:3.42-4.el9                             appstream                   215 k
 perl-Pod-Usage                         noarch               4:2.01-4.el9                             appstream                    40 k
 perl-Scalar-List-Utils                 x86_64               4:1.56-462.el9                           appstream                    70 k
 perl-SelectSaver                       noarch               1.02-481.el9                             appstream                    10 k
 perl-Socket                            x86_64               4:2.031-4.el9                            appstream                    54 k
 perl-Storable                          x86_64               1:3.21-460.el9                           appstream                    95 k
 perl-Symbol                            noarch               1.08-481.el9                             appstream                    13 k
 perl-Term-ANSIColor                    noarch               5.01-461.el9                             appstream                    48 k
 perl-Term-Cap                          noarch               1.17-460.el9                             appstream                    22 k
 perl-Text-ParseWords                   noarch               3.30-460.el9                             appstream                    16 k
 perl-Text-Tabs+Wrap                    noarch               2013.0523-460.el9                        appstream                    23 k
 perl-Time-Local                        noarch               2:1.300-7.el9                            appstream                    33 k
 perl-URI                               noarch               5.09-3.el9                               appstream                   108 k
 perl-base                              noarch               2.27-481.el9                             appstream                    15 k
 perl-constant                          noarch               1.33-461.el9                             appstream                    23 k
 perl-if                                noarch               0.60.800-481.el9                         appstream                    13 k
 perl-interpreter                       x86_64               4:5.32.1-481.el9                         appstream                    70 k
 perl-libnet                            noarch               3.13-4.el9                               appstream                   125 k
 perl-libs                              x86_64               4:5.32.1-481.el9                         appstream                   2.0 M
 perl-mro                               x86_64               1.23-481.el9                             appstream                    27 k
 perl-overload                          noarch               1.31-481.el9                             appstream                    44 k
 perl-overloading                       noarch               0.02-481.el9                             appstream                    11 k
 perl-parent                            noarch               1:0.238-460.el9                          appstream                    14 k
 perl-podlators                         noarch               1:4.14-460.el9                           appstream                   112 k
 perl-subs                              noarch               1.03-481.el9                             appstream                    10 k
 perl-vars                              noarch               1.05-481.el9                             appstream                    12 k
Installing weak dependencies:
 perl-NDBM_File                         x86_64               1.15-481.el9                             appstream                    21 k

Transaction Summary
========================================================================================================================================
Install  63 Packages
Upgrade   2 Packages

Total download size: 69 M
Downloading Packages:
[MIRROR] kmod-lustre-2.16.1-1.el9.x86_64.rpm: Curl error (28): Timeout was reached for https://downloads.whamcloud.com/public/lustre/lustre-2.16.1/el9.4/server/RPMS/x86_64/kmod-lustre-2.16.1-1.el9.x86_64.rpm [Operation too slow. Less than 1000 bytes/sec transferred the last 30 seconds]
(1/65): perl-Text-ParseWords-3.30-460.el9.noarch.rpm                                                     76 kB/s |  16 kB     00:00    
(2/65): perl-Exporter-5.74-461.el9.noarch.rpm                                                           223 kB/s |  31 kB     00:00    
(3/65): perl-Pod-Simple-3.42-4.el9.noarch.rpm                                                           747 kB/s | 215 kB     00:00    
(4/65): perl-File-Path-2.18-4.el9.noarch.rpm                                                             58 kB/s |  35 kB     00:00    
(5/65): perl-Pod-Perldoc-3.28.01-461.el9.noarch.rpm                                                      23 kB/s |  83 kB     00:03    
(6/65): perl-Getopt-Long-2.52-4.el9.noarch.rpm                                                           95 kB/s |  60 kB     00:00    
(7/65): perl-Pod-Usage-2.01-4.el9.noarch.rpm                                                            206 kB/s |  40 kB     00:00    
(8/65): perl-IO-Socket-IP-0.41-5.el9.noarch.rpm                                                         249 kB/s |  42 kB     00:00    
(9/65): perl-Time-Local-1.300-7.el9.noarch.rpm                                                          221 kB/s |  33 kB     00:00    
(10/65): perl-libnet-3.13-4.el9.noarch.rpm                                                              648 kB/s | 125 kB     00:00    
(11/65): perl-Carp-1.50-460.el9.noarch.rpm                                                              233 kB/s |  29 kB     00:00    
(12/65): perl-podlators-4.14-460.el9.noarch.rpm                                                         563 kB/s | 112 kB     00:00    
(13/65): perl-Term-Cap-1.17-460.el9.noarch.rpm                                                          114 kB/s |  22 kB     00:00    
(14/65): perl-Term-ANSIColor-5.01-461.el9.noarch.rpm                                                    419 kB/s |  48 kB     00:00    
(15/65): perl-HTTP-Tiny-0.076-462.el9.noarch.rpm                                                        330 kB/s |  53 kB     00:00    
(16/65): perl-Digest-1.19-4.el9.noarch.rpm                                                              235 kB/s |  25 kB     00:00    
(17/65): perl-URI-5.09-3.el9.noarch.rpm                                                                 548 kB/s | 108 kB     00:00    
(18/65): perl-constant-1.33-461.el9.noarch.rpm                                                          152 kB/s |  23 kB     00:00    
(19/65): perl-Encode-3.08-462.el9.x86_64.rpm                                                            494 kB/s | 1.7 MB     00:03    
(20/65): perl-Data-Dumper-2.174-462.el9.x86_64.rpm                                                      277 kB/s |  55 kB     00:00    
(21/65): perl-Scalar-List-Utils-1.56-462.el9.x86_64.rpm                                                 247 kB/s |  70 kB     00:00    
(22/65): perl-IO-Socket-SSL-2.073-2.el9.noarch.rpm                                                      609 kB/s | 214 kB     00:00    
(23/65): perl-Storable-3.21-460.el9.x86_64.rpm                                                          257 kB/s |  95 kB     00:00    
(24/65): perl-PathTools-3.78-461.el9.x86_64.rpm                                                          97 kB/s |  85 kB     00:00    
(25/65): perl-Mozilla-CA-20200520-6.el9.noarch.rpm                                                       77 kB/s |  12 kB     00:00    
(26/65): perl-Text-Tabs+Wrap-2013.0523-460.el9.noarch.rpm                                               188 kB/s |  23 kB     00:00    
(27/65): perl-Digest-MD5-2.58-4.el9.x86_64.rpm                                                          247 kB/s |  36 kB     00:00    
(28/65): perl-Pod-Escapes-1.07-460.el9.noarch.rpm                                                        96 kB/s |  20 kB     00:00    
(29/65): perl-MIME-Base64-3.16-4.el9.x86_64.rpm                                                         206 kB/s |  30 kB     00:00    
(30/65): perl-File-Temp-0.231.100-4.el9.noarch.rpm                                                      278 kB/s |  59 kB     00:00    
(31/65): perl-Socket-2.031-4.el9.x86_64.rpm                                                             251 kB/s |  54 kB     00:00    
(32/65): perl-mro-1.23-481.el9.x86_64.rpm                                                               6.7 kB/s |  27 kB     00:04    
(33/65): perl-libs-5.32.1-481.el9.x86_64.rpm                                                            333 kB/s | 2.0 MB     00:06    
(34/65): perl-interpreter-5.32.1-481.el9.x86_64.rpm                                                     186 kB/s |  70 kB     00:00    
(35/65): perl-POSIX-1.94-481.el9.x86_64.rpm                                                             256 kB/s |  95 kB     00:00    
(36/65): perl-NDBM_File-1.15-481.el9.x86_64.rpm                                                          63 kB/s |  21 kB     00:00    
(37/65): perl-IO-1.43-481.el9.x86_64.rpm                                                                260 kB/s |  85 kB     00:00    
(38/65): perl-Fcntl-1.13-481.el9.x86_64.rpm                                                              52 kB/s |  19 kB     00:00    
(39/65): perl-Errno-1.30-481.el9.x86_64.rpm                                                             117 kB/s |  13 kB     00:00    
(40/65): perl-B-1.80-481.el9.x86_64.rpm                                                                  48 kB/s | 178 kB     00:03    
(41/65): perl-vars-1.05-481.el9.noarch.rpm                                                               29 kB/s |  12 kB     00:00    
[MIRROR] perl-subs-1.03-481.el9.noarch.rpm: Curl error (28): Timeout was reached for http://mirror.nju.edu.cn/rocky/9.5/AppStream/x86_64/os/Packages/p/perl-subs-1.03-481.el9.noarch.rpm [Operation too slow. Less than 1000 bytes/sec transferred the last 30 seconds]
(42/65): perl-subs-1.03-481.el9.noarch.rpm                                                              333  B/s |  10 kB     00:31    
(43/65): perl-overloading-0.02-481.el9.noarch.rpm                                                        17 kB/s |  11 kB     00:00    
(44/65): perl-overload-1.31-481.el9.noarch.rpm                                                           16 kB/s |  44 kB     00:02    
(45/65): perl-if-0.60.800-481.el9.noarch.rpm                                                            5.1 kB/s |  13 kB     00:02    
(46/65): perl-base-2.27-481.el9.noarch.rpm                                                              6.0 kB/s |  15 kB     00:02    
(47/65): perl-Symbol-1.08-481.el9.noarch.rpm                                                             16 kB/s |  13 kB     00:00    
(48/65): perl-SelectSaver-1.02-481.el9.noarch.rpm                                                        20 kB/s |  10 kB     00:00    
(49/65): perl-IPC-Open3-1.21-481.el9.noarch.rpm                                                          19 kB/s |  21 kB     00:01    
(50/65): perl-Getopt-Std-1.12-481.el9.noarch.rpm                                                         22 kB/s |  14 kB     00:00    
(51/65): perl-FileHandle-2.03-481.el9.noarch.rpm                                                         57 kB/s |  14 kB     00:00    
(52/65): perl-File-stat-1.09-481.el9.noarch.rpm                                                          37 kB/s |  16 kB     00:00    
(53/65): perl-File-Basename-2.85-481.el9.noarch.rpm                                                      39 kB/s |  16 kB     00:00    
(54/65): perl-Class-Struct-0.66-481.el9.noarch.rpm                                                       89 kB/s |  21 kB     00:00    
(55/65): perl-AutoLoader-5.74-481.el9.noarch.rpm                                                         47 kB/s |  20 kB     00:00    
(56/65): perl-Net-SSLeay-1.94-1.el9.x86_64.rpm                                                          153 kB/s | 391 kB     00:02    
(57/65): perl-parent-0.238-460.el9.noarch.rpm                                                           9.9 kB/s |  14 kB     00:01    
(58/65): openssl-libs-3.2.2-6.el9_5.1.x86_64.rpm                                                         51 kB/s | 2.4 MB     00:47    
(59/65): openssl-3.2.2-6.el9_5.1.x86_64.rpm                                                              56 kB/s | 1.3 MB     00:23    
(60/65): kernel-core-5.14.0-427.31.1_lustre.el9.x86_64.rpm                                               80 kB/s |  20 MB     04:12    
(61/65): kmod-lustre-2.16.1-1.el9.x86_64.rpm                                                             21 kB/s | 5.2 MB     04:17    
(62/65): kmod-lustre-osd-ldiskfs-2.16.1-1.el9.x86_64.rpm                                                864 kB/s | 738 kB     00:00    
(63/65): lustre-2.16.1-1.el9.x86_64.rpm                                                                 1.1 MB/s | 977 kB     00:00    
(64/65): lustre-osd-ldiskfs-mount-2.16.1-1.el9.x86_64.rpm                                               8.6 kB/s |  20 kB     00:02    
(65/65): kernel-modules-core-5.14.0-427.31.1_lustre.el9.x86_64.rpm                                       98 kB/s |  32 MB     05:41    
----------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                   208 kB/s |  69 MB     05:42     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                1/1 
  Upgrading        : openssl-libs-1:3.2.2-6.el9_5.1.x86_64                                                                         1/67 
  Installing       : kernel-modules-core-5.14.0-427.31.1_lustre.el9.x86_64                                                         2/67 
  Installing       : kernel-core-5.14.0-427.31.1_lustre.el9.x86_64                                                                 3/67 
  Running scriptlet: kernel-core-5.14.0-427.31.1_lustre.el9.x86_64                                                                 3/67 
  Installing       : kmod-lustre-2.16.1-1.el9.x86_64                                                                               4/67 
  Running scriptlet: kmod-lustre-2.16.1-1.el9.x86_64                                                                               4/67 
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol __ib_alloc_pd
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_resolve_addr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_set_service_type
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_dereg_mr_user
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_reject
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_disconnect
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol __rdma_create_kernel_id
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_register_event_handler
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_resolve_route
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_unregister_event_handler
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_bind_addr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_create_qp
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_map_mr_sg
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_query_port
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_notify
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_listen
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_destroy_qp
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol __ib_create_cq
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_alloc_mr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_connect_locked
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_set_reuseaddr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_destroy_cq_user
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_modify_qp
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_dma_virt_map_sg
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_destroy_id
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_accept
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_dealloc_pd_user
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol __ib_alloc_pd
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_resolve_addr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_set_service_type
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_dereg_mr_user
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_reject
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_disconnect
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol __rdma_create_kernel_id
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_register_event_handler
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_resolve_route
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_unregister_event_handler
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_bind_addr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_create_qp
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_map_mr_sg
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_query_port
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_notify
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_listen
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_destroy_qp
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol __ib_create_cq
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_alloc_mr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_connect_locked
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_set_reuseaddr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_destroy_cq_user
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_modify_qp
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_dma_virt_map_sg
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_destroy_id
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_accept
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_dealloc_pd_user

  Installing       : perl-Digest-1.19-4.el9.noarch                                                                                 5/67 
  Installing       : perl-Digest-MD5-2.58-4.el9.x86_64                                                                             6/67 
  Installing       : perl-B-1.80-481.el9.x86_64                                                                                    7/67 
  Installing       : perl-FileHandle-2.03-481.el9.noarch                                                                           8/67 
  Installing       : perl-Data-Dumper-2.174-462.el9.x86_64                                                                         9/67 
  Installing       : perl-libnet-3.13-4.el9.noarch                                                                                10/67 
  Installing       : perl-base-2.27-481.el9.noarch                                                                                11/67 
  Installing       : perl-AutoLoader-5.74-481.el9.noarch                                                                          12/67 
  Installing       : perl-URI-5.09-3.el9.noarch                                                                                   13/67 
  Installing       : perl-Mozilla-CA-20200520-6.el9.noarch                                                                        14/67 
  Installing       : perl-Text-Tabs+Wrap-2013.0523-460.el9.noarch                                                                 15/67 
  Installing       : perl-Pod-Escapes-1:1.07-460.el9.noarch                                                                       16/67 
  Installing       : perl-if-0.60.800-481.el9.noarch                                                                              17/67 
  Installing       : perl-File-Path-2.18-4.el9.noarch                                                                             18/67 
  Installing       : perl-IO-Socket-IP-0.41-5.el9.noarch                                                                          19/67 
  Installing       : perl-Net-SSLeay-1.94-1.el9.x86_64                                                                            20/67 
  Installing       : perl-Time-Local-2:1.300-7.el9.noarch                                                                         21/67 
  Installing       : perl-IO-Socket-SSL-2.073-2.el9.noarch                                                                        22/67 
  Installing       : perl-Term-ANSIColor-5.01-461.el9.noarch                                                                      23/67 
  Installing       : perl-POSIX-1.94-481.el9.x86_64                                                                               24/67 
  Installing       : perl-Term-Cap-1.17-460.el9.noarch                                                                            25/67 
  Installing       : perl-subs-1.03-481.el9.noarch                                                                                26/67 
  Installing       : perl-Pod-Simple-1:3.42-4.el9.noarch                                                                          27/67 
  Installing       : perl-IPC-Open3-1.21-481.el9.noarch                                                                           28/67 
  Installing       : perl-Class-Struct-0.66-481.el9.noarch                                                                        29/67 
  Installing       : perl-HTTP-Tiny-0.076-462.el9.noarch                                                                          30/67 
  Installing       : perl-File-Temp-1:0.231.100-4.el9.noarch                                                                      31/67 
  Installing       : perl-Socket-4:2.031-4.el9.x86_64                                                                             32/67 
  Installing       : perl-Symbol-1.08-481.el9.noarch                                                                              33/67 
  Installing       : perl-SelectSaver-1.02-481.el9.noarch                                                                         34/67 
  Installing       : perl-File-stat-1.09-481.el9.noarch                                                                           35/67 
  Installing       : perl-podlators-1:4.14-460.el9.noarch                                                                         36/67 
  Installing       : perl-Pod-Perldoc-3.28.01-461.el9.noarch                                                                      37/67 
  Installing       : perl-mro-1.23-481.el9.x86_64                                                                                 38/67 
  Installing       : perl-Fcntl-1.13-481.el9.x86_64                                                                               39/67 
  Installing       : perl-overloading-0.02-481.el9.noarch                                                                         40/67 
  Installing       : perl-IO-1.43-481.el9.x86_64                                                                                  41/67 
  Installing       : perl-Pod-Usage-4:2.01-4.el9.noarch                                                                           42/67 
  Installing       : perl-Text-ParseWords-3.30-460.el9.noarch                                                                     43/67 
  Installing       : perl-constant-1.33-461.el9.noarch                                                                            44/67 
  Installing       : perl-Scalar-List-Utils-4:1.56-462.el9.x86_64                                                                 45/67 
  Installing       : perl-MIME-Base64-3.16-4.el9.x86_64                                                                           46/67 
  Installing       : perl-Errno-1.30-481.el9.x86_64                                                                               47/67 
  Installing       : perl-vars-1.05-481.el9.noarch                                                                                48/67 
  Installing       : perl-overload-1.31-481.el9.noarch                                                                            49/67 
  Installing       : perl-Getopt-Std-1.12-481.el9.noarch                                                                          50/67 
  Installing       : perl-File-Basename-2.85-481.el9.noarch                                                                       51/67 
  Installing       : perl-Storable-1:3.21-460.el9.x86_64                                                                          52/67 
  Installing       : perl-parent-1:0.238-460.el9.noarch                                                                           53/67 
  Installing       : perl-Getopt-Long-1:2.52-4.el9.noarch                                                                         54/67 
  Installing       : perl-Exporter-5.74-461.el9.noarch                                                                            55/67 
  Installing       : perl-Carp-1.50-460.el9.noarch                                                                                56/67 
  Installing       : perl-NDBM_File-1.15-481.el9.x86_64                                                                           57/67 
  Installing       : perl-PathTools-3.78-461.el9.x86_64                                                                           58/67 
  Installing       : perl-Encode-4:3.08-462.el9.x86_64                                                                            59/67 
  Installing       : perl-libs-4:5.32.1-481.el9.x86_64                                                                            60/67 
  Installing       : perl-interpreter-4:5.32.1-481.el9.x86_64                                                                     61/67 
  Installing       : lustre-osd-ldiskfs-mount-2.16.1-1.el9.x86_64                                                                 62/67 
  Installing       : kmod-lustre-osd-ldiskfs-2.16.1-1.el9.x86_64                                                                  63/67 
  Running scriptlet: kmod-lustre-osd-ldiskfs-2.16.1-1.el9.x86_64                                                                  63/67 
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol __ib_alloc_pd
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_resolve_addr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_set_service_type
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_dereg_mr_user
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_reject
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_disconnect
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol __rdma_create_kernel_id
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_register_event_handler
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_resolve_route
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_unregister_event_handler
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_bind_addr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_create_qp
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_map_mr_sg
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_query_port
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_notify
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_listen
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_destroy_qp
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol __ib_create_cq
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_alloc_mr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_connect_locked
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_set_reuseaddr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_destroy_cq_user
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_modify_qp
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_dma_virt_map_sg
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_destroy_id
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol rdma_accept
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/ko2iblnd.ko needs unknown symbol ib_dealloc_pd_user
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol __ib_alloc_pd
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_resolve_addr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_set_service_type
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_dereg_mr_user
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_reject
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_disconnect
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol __rdma_create_kernel_id
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_register_event_handler
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_resolve_route
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_unregister_event_handler
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_bind_addr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_create_qp
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_map_mr_sg
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_query_port
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_notify
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_listen
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_destroy_qp
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol __ib_create_cq
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_alloc_mr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_connect_locked
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_set_reuseaddr
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_destroy_cq_user
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_modify_qp
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_dma_virt_map_sg
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_destroy_id
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol rdma_accept
depmod: WARNING: /lib/modules/5.14.0-427.31.1_lustre.el9.x86_64/extra/lustre/net/in-kernel-ko2iblnd.ko needs unknown symbol ib_dealloc_pd_user

  Installing       : lustre-2.16.1-1.el9.x86_64                                                                                   64/67 
  Running scriptlet: lustre-2.16.1-1.el9.x86_64                                                                                   64/67 
  Upgrading        : openssl-1:3.2.2-6.el9_5.1.x86_64                                                                             65/67 
  Cleanup          : openssl-1:3.0.7-27.el9.x86_64                                                                                66/67 
  Cleanup          : openssl-libs-1:3.0.7-27.el9.x86_64                                                                           67/67 
  Running scriptlet: kernel-modules-core-5.14.0-427.31.1_lustre.el9.x86_64                                                        67/67 
  Running scriptlet: kernel-core-5.14.0-427.31.1_lustre.el9.x86_64                                                                67/67 
  Running scriptlet: openssl-libs-1:3.0.7-27.el9.x86_64                                                                           67/67 
  Verifying        : kernel-core-5.14.0-427.31.1_lustre.el9.x86_64                                                                 1/67 
  Verifying        : kernel-modules-core-5.14.0-427.31.1_lustre.el9.x86_64                                                         2/67 
  Verifying        : kmod-lustre-2.16.1-1.el9.x86_64                                                                               3/67 
  Verifying        : kmod-lustre-osd-ldiskfs-2.16.1-1.el9.x86_64                                                                   4/67 
  Verifying        : lustre-2.16.1-1.el9.x86_64                                                                                    5/67 
  Verifying        : lustre-osd-ldiskfs-mount-2.16.1-1.el9.x86_64                                                                  6/67 
  Verifying        : perl-Text-ParseWords-3.30-460.el9.noarch                                                                      7/67 
  Verifying        : perl-Exporter-5.74-461.el9.noarch                                                                             8/67 
  Verifying        : perl-Pod-Simple-1:3.42-4.el9.noarch                                                                           9/67 
  Verifying        : perl-File-Path-2.18-4.el9.noarch                                                                             10/67 
  Verifying        : perl-Pod-Perldoc-3.28.01-461.el9.noarch                                                                      11/67 
  Verifying        : perl-Getopt-Long-1:2.52-4.el9.noarch                                                                         12/67 
  Verifying        : perl-Pod-Usage-4:2.01-4.el9.noarch                                                                           13/67 
  Verifying        : perl-IO-Socket-IP-0.41-5.el9.noarch                                                                          14/67 
  Verifying        : perl-Time-Local-2:1.300-7.el9.noarch                                                                         15/67 
  Verifying        : perl-libnet-3.13-4.el9.noarch                                                                                16/67 
  Verifying        : perl-Carp-1.50-460.el9.noarch                                                                                17/67 
  Verifying        : perl-podlators-1:4.14-460.el9.noarch                                                                         18/67 
  Verifying        : perl-Term-Cap-1.17-460.el9.noarch                                                                            19/67 
  Verifying        : perl-Term-ANSIColor-5.01-461.el9.noarch                                                                      20/67 
  Verifying        : perl-HTTP-Tiny-0.076-462.el9.noarch                                                                          21/67 
  Verifying        : perl-Digest-1.19-4.el9.noarch                                                                                22/67 
  Verifying        : perl-URI-5.09-3.el9.noarch                                                                                   23/67 
  Verifying        : perl-constant-1.33-461.el9.noarch                                                                            24/67 
  Verifying        : perl-Encode-4:3.08-462.el9.x86_64                                                                            25/67 
  Verifying        : perl-Data-Dumper-2.174-462.el9.x86_64                                                                        26/67 
  Verifying        : perl-Scalar-List-Utils-4:1.56-462.el9.x86_64                                                                 27/67 
  Verifying        : perl-IO-Socket-SSL-2.073-2.el9.noarch                                                                        28/67 
  Verifying        : perl-Storable-1:3.21-460.el9.x86_64                                                                          29/67 
  Verifying        : perl-PathTools-3.78-461.el9.x86_64                                                                           30/67 
  Verifying        : perl-Mozilla-CA-20200520-6.el9.noarch                                                                        31/67 
  Verifying        : perl-Text-Tabs+Wrap-2013.0523-460.el9.noarch                                                                 32/67 
  Verifying        : perl-Digest-MD5-2.58-4.el9.x86_64                                                                            33/67 
  Verifying        : perl-Pod-Escapes-1:1.07-460.el9.noarch                                                                       34/67 
  Verifying        : perl-MIME-Base64-3.16-4.el9.x86_64                                                                           35/67 
  Verifying        : perl-File-Temp-1:0.231.100-4.el9.noarch                                                                      36/67 
  Verifying        : perl-Socket-4:2.031-4.el9.x86_64                                                                             37/67 
  Verifying        : perl-mro-1.23-481.el9.x86_64                                                                                 38/67 
  Verifying        : perl-libs-4:5.32.1-481.el9.x86_64                                                                            39/67 
  Verifying        : perl-interpreter-4:5.32.1-481.el9.x86_64                                                                     40/67 
  Verifying        : perl-POSIX-1.94-481.el9.x86_64                                                                               41/67 
  Verifying        : perl-NDBM_File-1.15-481.el9.x86_64                                                                           42/67 
  Verifying        : perl-IO-1.43-481.el9.x86_64                                                                                  43/67 
  Verifying        : perl-Fcntl-1.13-481.el9.x86_64                                                                               44/67 
  Verifying        : perl-Errno-1.30-481.el9.x86_64                                                                               45/67 
  Verifying        : perl-B-1.80-481.el9.x86_64                                                                                   46/67 
  Verifying        : perl-vars-1.05-481.el9.noarch                                                                                47/67 
  Verifying        : perl-subs-1.03-481.el9.noarch                                                                                48/67 
  Verifying        : perl-overloading-0.02-481.el9.noarch                                                                         49/67 
  Verifying        : perl-overload-1.31-481.el9.noarch                                                                            50/67 
  Verifying        : perl-if-0.60.800-481.el9.noarch                                                                              51/67 
  Verifying        : perl-base-2.27-481.el9.noarch                                                                                52/67 
  Verifying        : perl-Symbol-1.08-481.el9.noarch                                                                              53/67 
  Verifying        : perl-SelectSaver-1.02-481.el9.noarch                                                                         54/67 
  Verifying        : perl-IPC-Open3-1.21-481.el9.noarch                                                                           55/67 
  Verifying        : perl-Getopt-Std-1.12-481.el9.noarch                                                                          56/67 
  Verifying        : perl-FileHandle-2.03-481.el9.noarch                                                                          57/67 
  Verifying        : perl-File-stat-1.09-481.el9.noarch                                                                           58/67 
  Verifying        : perl-File-Basename-2.85-481.el9.noarch                                                                       59/67 
  Verifying        : perl-Class-Struct-0.66-481.el9.noarch                                                                        60/67 
  Verifying        : perl-AutoLoader-5.74-481.el9.noarch                                                                          61/67 
  Verifying        : perl-Net-SSLeay-1.94-1.el9.x86_64                                                                            62/67 
  Verifying        : perl-parent-1:0.238-460.el9.noarch                                                                           63/67 
  Verifying        : openssl-libs-1:3.2.2-6.el9_5.1.x86_64                                                                        64/67 
  Verifying        : openssl-libs-1:3.0.7-27.el9.x86_64                                                                           65/67 
  Verifying        : openssl-1:3.2.2-6.el9_5.1.x86_64                                                                             66/67 
  Verifying        : openssl-1:3.0.7-27.el9.x86_64                                                                                67/67 

Upgraded:
  openssl-1:3.2.2-6.el9_5.1.x86_64                                 openssl-libs-1:3.2.2-6.el9_5.1.x86_64                                
Installed:
  kernel-core-5.14.0-427.31.1_lustre.el9.x86_64                  kernel-modules-core-5.14.0-427.31.1_lustre.el9.x86_64                 
  kmod-lustre-2.16.1-1.el9.x86_64                                kmod-lustre-osd-ldiskfs-2.16.1-1.el9.x86_64                           
  lustre-2.16.1-1.el9.x86_64                                     lustre-osd-ldiskfs-mount-2.16.1-1.el9.x86_64                          
  perl-AutoLoader-5.74-481.el9.noarch                            perl-B-1.80-481.el9.x86_64                                            
  perl-Carp-1.50-460.el9.noarch                                  perl-Class-Struct-0.66-481.el9.noarch                                 
  perl-Data-Dumper-2.174-462.el9.x86_64                          perl-Digest-1.19-4.el9.noarch                                         
  perl-Digest-MD5-2.58-4.el9.x86_64                              perl-Encode-4:3.08-462.el9.x86_64                                     
  perl-Errno-1.30-481.el9.x86_64                                 perl-Exporter-5.74-461.el9.noarch                                     
  perl-Fcntl-1.13-481.el9.x86_64                                 perl-File-Basename-2.85-481.el9.noarch                                
  perl-File-Path-2.18-4.el9.noarch                               perl-File-Temp-1:0.231.100-4.el9.noarch                               
  perl-File-stat-1.09-481.el9.noarch                             perl-FileHandle-2.03-481.el9.noarch                                   
  perl-Getopt-Long-1:2.52-4.el9.noarch                           perl-Getopt-Std-1.12-481.el9.noarch                                   
  perl-HTTP-Tiny-0.076-462.el9.noarch                            perl-IO-1.43-481.el9.x86_64                                           
  perl-IO-Socket-IP-0.41-5.el9.noarch                            perl-IO-Socket-SSL-2.073-2.el9.noarch                                 
  perl-IPC-Open3-1.21-481.el9.noarch                             perl-MIME-Base64-3.16-4.el9.x86_64                                    
  perl-Mozilla-CA-20200520-6.el9.noarch                          perl-NDBM_File-1.15-481.el9.x86_64                                    
  perl-Net-SSLeay-1.94-1.el9.x86_64                              perl-POSIX-1.94-481.el9.x86_64                                        
  perl-PathTools-3.78-461.el9.x86_64                             perl-Pod-Escapes-1:1.07-460.el9.noarch                                
  perl-Pod-Perldoc-3.28.01-461.el9.noarch                        perl-Pod-Simple-1:3.42-4.el9.noarch                                   
  perl-Pod-Usage-4:2.01-4.el9.noarch                             perl-Scalar-List-Utils-4:1.56-462.el9.x86_64                          
  perl-SelectSaver-1.02-481.el9.noarch                           perl-Socket-4:2.031-4.el9.x86_64                                      
  perl-Storable-1:3.21-460.el9.x86_64                            perl-Symbol-1.08-481.el9.noarch                                       
  perl-Term-ANSIColor-5.01-461.el9.noarch                        perl-Term-Cap-1.17-460.el9.noarch                                     
  perl-Text-ParseWords-3.30-460.el9.noarch                       perl-Text-Tabs+Wrap-2013.0523-460.el9.noarch                          
  perl-Time-Local-2:1.300-7.el9.noarch                           perl-URI-5.09-3.el9.noarch                                            
  perl-base-2.27-481.el9.noarch                                  perl-constant-1.33-461.el9.noarch                                     
  perl-if-0.60.800-481.el9.noarch                                perl-interpreter-4:5.32.1-481.el9.x86_64                              
  perl-libnet-3.13-4.el9.noarch                                  perl-libs-4:5.32.1-481.el9.x86_64                                     
  perl-mro-1.23-481.el9.x86_64                                   perl-overload-1.31-481.el9.noarch                                     
  perl-overloading-0.02-481.el9.noarch                           perl-parent-1:0.238-460.el9.noarch                                    
  perl-podlators-1:4.14-460.el9.noarch                           perl-subs-1.03-481.el9.noarch                                         
  perl-vars-1.05-481.el9.noarch                                 

Complete!


[root@el9-1 default]# uname -a 
Linux el9-1 5.14.0-427.18.1.el9_4.x86_64 #1 SMP PREEMPT_DYNAMIC Mon May 27 16:35:12 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux
[root@el9-1 default]# reboot
Connection to 192.168.122.179 closed by remote host.
Connection to 192.168.122.179 closed.
hujun@deepin1:~/env/local$ ./rock9.sh 
Activate the web console with: systemctl enable --now cockpit.socket

Last login: Sat May 10 07:58:24 2025 from 192.168.122.1
[root@el9-1 ~]# uname -a 
Linux el9-1 5.14.0-427.31.1_lustre.el9.x86_64 #1 SMP PREEMPT_DYNAMIC Sat Nov 16 02:13:15 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux
```


[root@el9-1 ~]# sudo parted -s /dev/vdb mklabel gpt \
  mkpart primary 0GB 33GB \
  mkpart primary 33GB 66GB \
  mkpart primary 66GB 100GB
[root@el9-1 ~]# parted --help 
Usage: parted [OPTION]... [DEVICE [COMMAND [PARAMETERS]...]...]
Apply COMMANDs with PARAMETERS to DEVICE.  If no COMMAND(s) are given, run in
interactive mode.

OPTIONs:
  -h, --help                      displays this help message
  -l, --list                      lists partition layout on all block devices
  -m, --machine                   displays machine parseable output
  -j, --json                      displays JSON output
  -s, --script                    never prompts for user intervention
  -f, --fix                       in script mode, fix instead of abort when asked
  -v, --version                   displays the version
  -a, --align=[none|cyl|min|opt]  alignment for new partitions

COMMANDs:
  align-check TYPE N                       check partition N for TYPE(min|opt)
        alignment
  help [COMMAND]                           print general help, or help on
        COMMAND
  mklabel,mktable LABEL-TYPE               create a new disklabel (partition
        table)
  mkpart PART-TYPE [FS-TYPE] START END     make a partition
  name NUMBER NAME                         name partition NUMBER as NAME
  print [devices|free|list,all]            display the partition table, or
        available devices, or free space, or all found partitions
  quit                                     exit program
  rescue START END                         rescue a lost partition near START
        and END
  resizepart NUMBER END                    resize partition NUMBER
  rm NUMBER                                delete partition NUMBER
  select DEVICE                            choose the device to edit
  disk_set FLAG STATE                      change the FLAG on selected device
  disk_toggle [FLAG]                       toggle the state of FLAG on selected
        device
  set NUMBER FLAG STATE                    change the FLAG on partition NUMBER
  toggle [NUMBER [FLAG]]                   toggle the state of FLAG on partition
        NUMBER
  type NUMBER TYPE-ID or TYPE-UUID         type set TYPE-ID or TYPE-UUID of
        partition NUMBER
  unit UNIT                                set the default unit to UNIT
  version                                  display the version number and
        copyright information of GNU Parted

Report bugs to bug-parted@gnu.org
[root@el9-1 ~]# parted -l /dev/vdb 
Model: Virtio Block Device (virtblk)
Disk /dev/vdb: 107GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 

Number  Start   End     Size    File system  Name     Flags
 1      1049kB  33.0GB  33.0GB               primary
 2      33.0GB  66.0GB  33.0GB               primary
 3      66.0GB  100GB   34.0GB               primary


Model: Virtio Block Device (virtblk)
Disk /dev/vda: 10.7GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 

Number  Start   End     Size    File system  Name      Flags
 1      1049kB  3146kB  2097kB               p.legacy  bios_grub
 2      3146kB  108MB   105MB   fat16        p.UEFI    boot, esp
 3      108MB   1157MB  1049MB  xfs          p.lxboot  bls_boot
 4      1157MB  10.7GB  9581MB  xfs          p.lxroot


[root@el9-1 ~]# 


[root@el9-1 modprobe.d]# mkdir /mnt/vdb1
mkfs.lustre --fsname=lustrefs --mgsnode=192.168.122.179@tcp0 --mdt --mgs --index=0 --reformat /dev/vdb1
mount -o rw -o loop -t lustre /dev/vdb1 /mnt/vdb1

   Permanent disk data:
Target:     lustrefs:MDT0000
Index:      0
Lustre FS:  lustrefs
Mount type: ldiskfs
Flags:      0x65
              (MDT MGS first_time update )
Persistent mount opts: user_xattr,errors=remount-ro
Parameters: mgsnode=192.168.122.179@tcp

device size = 31470MB
formatting backing filesystem ldiskfs on /dev/vdb1
        target name   lustrefs:MDT0000
        kilobytes     32225280
        options        -J size=1258 -I 1024 -i 2560 -q -O uninit_bg,^extents,dirdata,dir_nlink,quota,project,huge_file,ea_inode,large_dir,^fast_commit,flex_bg -E lazy_journal_init,lazy_itable_init="0",packed_meta_blocks -F
mkfs_cmd = mke2fs -j -b 4096 -L lustrefs:MDT0000  -J size=1258 -I 1024 -i 2560 -q -O uninit_bg,^extents,dirdata,dir_nlink,quota,project,huge_file,ea_inode,large_dir,^fast_commit,flex_bg -E lazy_journal_init,lazy_itable_init="0",packed_meta_blocks -F /dev/vdb1 32225280k
Writing CONFIGS/mountdata



[root@el9-1 ~]# mkdir /mnt/vdb2
mkfs.lustre --fsname=lustrefs --mgsnode=192.168.122.179@tcp0 --ost --index=0 --reformat /dev/vdb2
mount -o rw -o loop -t lustre /dev/vdb2 /mnt/vdb2

   Permanent disk data:
Target:     lustrefs:OST0000
Index:      0
Lustre FS:  lustrefs
Mount type: ldiskfs
Flags:      0x62
              (OST first_time update )
Persistent mount opts: ,errors=remount-ro
Parameters: mgsnode=192.168.122.179@tcp

device size = 31472MB
formatting backing filesystem ldiskfs on /dev/vdb2
        target name   lustrefs:OST0000
        kilobytes     32227328
        options        -J size=1024 -I 512 -i 69905 -q -O uninit_bg,extents,dir_nlink,quota,project,huge_file,large_dir,^fast_commit,flex_bg -G 256 -E resize="4290772992",lazy_journal_init,lazy_itable_init="0",packed_meta_blocks -F
mkfs_cmd = mke2fs -j -b 4096 -L lustrefs:OST0000  -J size=1024 -I 512 -i 69905 -q -O uninit_bg,extents,dir_nlink,quota,project,huge_file,large_dir,^fast_commit,flex_bg -G 256 -E resize="4290772992",lazy_journal_init,lazy_itable_init="0",packed_meta_blocks -F /dev/vdb2 32227328k
Writing CONFIGS/mountdata
[root@el9-1 ~]# mount -t lustre 192.168.122.179@tcp:/lustrefs /mnt/lustre
warning: /mnt/lustre: cannot resolve: No such file or directory
[root@el9-1 ~]# mkdir -p /mnt/lustre
[root@el9-1 ~]# mount -t lustre 192.168.122.179@tcp:/lustrefs /mnt/lustre
[root@el9-1 ~]# cd /mnt/lustre/
[root@el9-1 lustre]# ls
[root@el9-1 lustre]# cp /bin/a*  . 
ls
[root@el9-1 lustre]# ls
addr2line  appstream-compose  apropos         ar    arping  audit2allow  aulast     ausyscall   auvirt
alias      appstream-util     apropos.man-db  arch  as      audit2why    aulastlog  authselect  awk
[root@el9-1 lustre]# ls
addr2line  appstream-compose  apropos         ar    arping  audit2allow  aulast     ausyscall   auvirt
alias      appstream-util     apropos.man-db  arch  as      audit2why    aulastlog  authselect  awk
[root@el9-1 lustre]# cat /etc/modprobe.d/lustre.conf 
options lnet networks=tcp0(eth0)
[root@el9-1 lustre]# lctl get_param lov.*-mdtlov.target_obd
lov.lustrefs-MDT0000-mdtlov.target_obd=0: lustrefs-OST0000_UUID ACTIVE


[root@el9-1 lustre]# lfs df -h 
UUID                       bytes        Used   Available Use% Mounted on
lustrefs-MDT0000_UUID       17.0G        2.8M       15.5G   1% /mnt/lustre[MDT:0] 
lustrefs-OST0000_UUID       29.2G        3.3M       27.7G   1% /mnt/lustre[OST:0] 

filesystem_summary:        29.2G        3.3M       27.7G   1% /mnt/lustre



[root@el9-1 lustre]# lctl --list-commands 
quit                exit                help                --help              
version             --version           list-commands       --list-commands     
--ignore_errors     ignore_errors       

===== metacommands =======
--device            

======== control =========
lustre_build_version 

===== network config =====
--net               network             net                 list_nids           
which_nid           replace_nids        interface_list      peer_list           
conn_list           route_list          show_route          ping                
net_drop_add        net_drop_del        net_drop_reset      net_drop_list       
net_delay_add       net_delay_del       net_delay_reset     net_delay_list      

==== obd device selection ====
device              cfg_device          device_list         dl                  

==== obd device operations ====
activate            deactivate          abort_recovery      abort_recovery_mdt  
recover             conf_param          get_param           set_param           
apply_yaml          list_param          del_ost             

==== debugging control ====
debug_daemon        debug_kernel        dk                  debug_file          
df                  clear               mark                filter              
show                debug_list          modules             

===  Pools ==
pool_new            pool_add            pool_remove         pool_destroy        
pool_list           

===  Barrier ==
barrier_freeze      barrier_thaw        barrier_stat        barrier_rescan      

===  Snapshot ==
snapshot_create     snapshot_destroy    snapshot_modify     snapshot_list       
snapshot_mount      snapshot_umount     

=== Nodemap ===
nodemap_activate    nodemap_add         nodemap_del         nodemap_add_range   
nodemap_del_range   nodemap_modify      nodemap_add_idmap   nodemap_del_idmap   
nodemap_set_fileset nodemap_set_sepol   nodemap_test_nid    nodemap_test_id     
nodemap_info        

===  Changelogs ==
changelog_register  changelog_deregister 

=== Persistent Client Cache ===
pcc                 

== device setup (these are not normally used post 1.4) ==
attach              detach              setup               cleanup             

==== LFSCK ====
lfsck_start         lfsck_stop          lfsck_query         lfsck               

==== LLOG ====
llog_catlist        llog_info           llog_print          llog_cancel         
llog_check          llog_remove         lcfg_clear          clear_conf          
lcfg_fork           fork_lcfg           lcfg_erase          erase_lcfg          

==== obsolete (DANGEROUS) ====
add_interface       del_interface       add_route           del_route           
set_route           

==== testing (DANGEROUS) ====
--threads           lookup              readonly            notransno           
add_uuid            del_uuid            add_peer            del_peer            
add_conn            del_conn            disconnect          push                
mynid               fail                test_create         test_mkdir          
test_destroy        test_rmdir          test_lookup         test_setxattr       
test_md_getattr     getattr             setattr             create              
destroy             test_getattr        test_setattr        test_brw            
getobjversion       

## issue ： Is the MGS running？

https://blog.csdn.net/qq_57973134/article/details/138033401


[root@el9-1 lustre]# lnetctl net show 
net:
-     net type: lo
      local NI(s):
      -     nid: 0@lo
            status: up
-     net type: tcp
      local NI(s):
      -     nid: 192.168.122.179@tcp
            status: up
            interfaces:
                  0: eth0
[root@el9-1 lustre]# 

