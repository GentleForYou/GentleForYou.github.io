
---
layout: post
title: 使用Moya库,进行https证书校验
date: 2018-06-15 13:00:00 
tags: swift
---

查了很多网上的文章,对moya的https证书校验基本都是略,要么就是16/17年的代码,但是运行的时候找到证书,转data格式的时候报错,崩溃; 
我用的Moya库版本号是11的,pod 'Moya', '~> 11.0'
不费话,下面直接看代码吧,希望对你们有帮助;
 ``` 
 public func defaultAlamofireManager() -> Manager {
    let configuration = URLSessionConfiguration.default
    configuration.httpAdditionalHeaders = Alamofire.SessionManager.defaultHTTPHeaders
    //获取本地证书
    let path: String = Bundle.main.path(forResource: "证书名", ofType: "cer")!
    let certificateData = try? Data(contentsOf: URL(fileURLWithPath: path)) as CFData
    let certificate = SecCertificateCreateWithData(nil, certificateData!)
    let certificates :[SecCertificate] = [certificate!]
    
    let policies: [String: ServerTrustPolicy] = [
        "域名" : .pinCertificates(certificates: certificates, validateCertificateChain: true, validateHost: true)
    ]
    let manager = Alamofire.SessionManager(configuration: configuration,serverTrustPolicyManager: ServerTrustPolicyManager(policies: policies))
    return manager
}
//把defaultAlamofireManager当参数传进去就行了
let kProvider = MoyaProvider<APIManager>(endpointClosure: myEndpointClosure, requestClosure: requestClosure, manager:defaultAlamofireManager(), plugins: [networkPlugin], trackInflights: false)
``` 

总阅读(<span id="busuanzi_value_page_pv"></span>)
