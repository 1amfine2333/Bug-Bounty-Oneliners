# Bug-Bounty-Oneliners
Oneliners curated from my experience and from the internet


### 一键获取http标题:(Update! HTTPX does a better job :-) )
```bash
for i in $(cat urls.txt ); do echo "$i | $(curl --connect-timeout 0.5 $i -so - | grep -iPo '(?<=<title>)(.*)(?=</title>)')"; done | tee -a titles.txt
```

### 从IP范围提取子域:
```bash
nmap IP_range | grep "domain" | awk '{print $5}'
```

### Find subdomains and takeover
```bash
subfinder -d {target} >> domains ; assetfinder -subs-only {target} >> domains ; amass enum -norecursive -noalts -d {target} >> domains ; subjack -w domains -t 100 -timeout 30 -ssl -c ~/fingerprints.json -v 3 >> takeover ;
```
### 从解压缩的APK中提取信息
```bash
apktool d apk;grep -EHir "accesskey|admin|aes|api_key|apikey|checkClientTrusted|crypt|http:|https:|password|pinning|secret|SHA256|SharedPreferences|superuser|token|X509TrustManager|insert into" APKfolder
```
### 收集所有网址，发送给burp
```bash
cat hosts | sed 's/https\?:\/\///' | gau > urls.txt
cat urls.txt | grep -P "\w+\.js(\?|$)" | sort -u > jsurls.txt
ffuf -mc 200 -w jsurls.txt:HFUZZ -u HFUZZ -replay-proxy http:127.0.0.1:8080
```
