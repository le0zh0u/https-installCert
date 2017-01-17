# https-installCert
To fix webService visit url with https certs, throws PKIX path building failed Exception.



Complie InstallCert.java and run `java InstallCert hostname` . Such as `java InstallCert ecc.fedora.redhat.com` . Then u will see :

```
java InstallCert ecc.fedora.redhat.com
Loading KeyStore /usr/jdk/instances/jdk1.5.0/jre/lib/security/cacerts...
Opening connection to ecc.fedora.redhat.com:443...
Starting SSL handshake...

javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
	at com.sun.net.ssl.internal.ssl.Alerts.getSSLException(Alerts.java:150)
	at com.sun.net.ssl.internal.ssl.SSLSocketImpl.fatal(SSLSocketImpl.java:1476)
	at com.sun.net.ssl.internal.ssl.Handshaker.fatalSE(Handshaker.java:174)
	at com.sun.net.ssl.internal.ssl.Handshaker.fatalSE(Handshaker.java:168)
	at com.sun.net.ssl.internal.ssl.ClientHandshaker.serverCertificate(ClientHandshaker.java:846)
	at com.sun.net.ssl.internal.ssl.ClientHandshaker.processMessage(ClientHandshaker.java:106)
	at com.sun.net.ssl.internal.ssl.Handshaker.processLoop(Handshaker.java:495)
	at com.sun.net.ssl.internal.ssl.Handshaker.process_record(Handshaker.java:433)
	at com.sun.net.ssl.internal.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:815)
	at com.sun.net.ssl.internal.ssl.SSLSocketImpl.performInitialHandshake(SSLSocketImpl.java:1025)
	at com.sun.net.ssl.internal.ssl.SSLSocketImpl.startHandshake(SSLSocketImpl.java:1038)
	at InstallCert.main(InstallCert.java:63)
Caused by: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
	at sun.security.validator.PKIXValidator.doBuild(PKIXValidator.java:221)
	at sun.security.validator.PKIXValidator.engineValidate(PKIXValidator.java:145)
	at sun.security.validator.Validator.validate(Validator.java:203)
	at com.sun.net.ssl.internal.ssl.X509TrustManagerImpl.checkServerTrusted(X509TrustManagerImpl.java:172)
	at InstallCert$SavingTrustManager.checkServerTrusted(InstallCert.java:158)
	at com.sun.net.ssl.internal.ssl.JsseX509TrustManager.checkServerTrusted(SSLContextImpl.java:320)
	at com.sun.net.ssl.internal.ssl.ClientHandshaker.serverCertificate(ClientHandshaker.java:839)
	... 7 more
Caused by: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
	at sun.security.provider.certpath.SunCertPathBuilder.engineBuild(SunCertPathBuilder.java:236)
	at java.security.cert.CertPathBuilder.build(CertPathBuilder.java:194)
	at sun.security.validator.PKIXValidator.doBuild(PKIXValidator.java:216)
	... 13 more

Server sent 2 certificate(s):

 1 Subject CN=ecc.fedora.redhat.com, O=example.com, C=US
   Issuer  CN=Certificate Shack, O=example.com, C=US
   sha1    2e 7f 76 9b 52 91 09 2e 5d 8f 6b 61 39 2d 5e 06 e4 d8 e9 c7 
   md5     dd d1 a8 03 d7 6c 4b 11 a7 3d 74 28 89 d0 67 54 

 2 Subject CN=Certificate Shack, O=example.com, C=US
   Issuer  CN=Certificate Shack, O=example.com, C=US
   sha1    fb 58 a7 03 c4 4e 3b 0e e3 2c 40 2f 87 64 13 4d df e1 a1 a6 
   md5     72 a0 95 43 7e 41 88 18 ae 2f 6d 98 01 2c 89 68 

Enter certificate to add to trusted keystore or 'q' to quit: [1]
```

Type 1, and type Enter. It will create a cert name `jssecacerts` in the current dir. Then copy it to `$JAVA_HOMT/jre/lib/security`  dir. It will work.



Ref: [PKIX path building failed 的问题](http://blog.csdn.net/mengxianhua/article/details/6045144)