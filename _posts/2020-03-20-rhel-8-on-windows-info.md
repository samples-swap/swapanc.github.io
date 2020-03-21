---
layout: post
published: false
title: RHEL 8 on Windows info
---
## get ip of running windows container
```
get-vm | Where-Object {$_.State -eq 'Running'} | Select -ExpandProperty Networkadapters
```   
   
## info on interactive bash commandlie here documents
```bash
rm -rf /tmp/kafka-connect-*; ls -rtl /tmp ;\
export tmpdir="/tmp/kafka-connect-${RANDOM}" ;\
echo "tmpdir: $tmpdir" ;\
export version_num="8.0.19" ;\
echo "version_num: $version_num" ;\
export prefix="mysql-connector-java-${version_num}" ;\
echo "prefix: $prefix" ;\
export url_prefix="https://dev.mysql.com/get/Downloads/Connector-J" ;\
echo "url prefix $url_prefix" ;\ 
export targz="${prefix}.tar.gz" ;\
export download_url="${url_prefix}/${targz}" ;\
echo $download_url ;\
mkdir $tmpdir; wget -P $tmpdir $download_url ; ls -rtl $tmpdir; cd $tmpdir ;\
export jar="${prefix}.jar" ;\
export extract_file_path="${prefix}/${jar}" ;\
tar -xf $targz --strip-components=1 $extract_file_path -C $tmpdir



export tmpdir="/tmp/kafka-connect-${RANDOM}" ;\
export version="8.0.19" ;\
export url_prefix='https://dev.mysql.com/get/Downloads/Connector-J' ;\
bash << EOF
echo $tmpdir
export driver="mysql-connector-java-${version}.tar.gz" 
export download_url="${url_prefix}/${driver}"
if [[ ! -d $tmpdir ]]; then if ! mkdir $tmpdir; then echo "error creating $tmpdir"; exit 1; fi ;fi
if ! cd $tmpdir; then echo "could not cd to $tmpdir"; fi
if ! wget -P "${tmpdir}/" -q $download_url ; then "echo could not download $driver to $tmpdir "; exit 1; fi
if tar -zxvf $tmpdir/$driver -C $tmpdir && tar -xf 
cd $tmpdir
ls -rtl $tmpdir
EOF
```   