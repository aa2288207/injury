title: Android Des加密
categories:
  - Android
date: 2014-05-21 03:21:12
tags:
  - Android
---

public class CrytoTools {
private static final byte[] DESkey = "encrykey".getBytes();// 设置密钥，略去
private static final byte[] DESIV = "encrypiv".getBytes();;// 设置向量，略去

static AlgorithmParameterSpec iv = null;// 加密算法的参数接口，IvParameterSpec是它的一个实现
private static Key key = null;

public CrytoTools() throws Exception {
DESKeySpec keySpec = new DESKeySpec(DESkey);// 设置密钥参数
iv = new IvParameterSpec(DESIV);// 设置向量
SecretKeyFactory keyFactory = SecretKeyFactory.getInstance("DES");// 获得密钥工厂
key = keyFactory.generateSecret(keySpec);// 得到密钥对象
}

public String encode(String data) throws Exception {
Cipher enCipher = Cipher.getInstance("DES/CBC/PKCS5Padding");// 得到加密对象Cipher
enCipher.init(Cipher.ENCRYPT_MODE, key, iv);// 设置工作模式为加密模式，给出密钥和向量
byte[] pasByte = enCipher.doFinal(data.getBytes("utf-8"));
return new String(Base64.encode(pasByte, Base64.DEFAULT));
}

public String decode(String data) throws Exception {
Cipher deCipher = Cipher.getInstance("DES/CBC/PKCS5Padding");
deCipher.init(Cipher.DECRYPT_MODE, key, iv);
byte[] pasByte = deCipher.doFinal(Base64.decode(data, Base64.DEFAULT));
return new String(pasByte,"utf-8");
}
}

&nbsp;