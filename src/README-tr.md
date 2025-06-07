# simple-java-app-pipeline-demo

## Yapılanlar
1. **İlk Commit & GitHub’a Push**  
   - `git init`, `pom.xml`, `src/`, `Jenkinsfile`  
   - Remote ekledik, master → main uyumunu sağladık  

2. **Jenkins’i Docker’da Çalıştırma**  
   - `docker pull jenkins/jenkins:lts`  
   - `docker run … jenkins/jenkins:lts`  
   - Unlock, önerilen eklentiler, ilk admin  

3. **Global Tool Configuration**  
   - Manage Jenkins → Araçlar → JDK11 ve Maven3 eklendi  

4. **Pipeline Job & Webhook**  
   - Yeni Pipeline işi: SCM’den `Jenkinsfile`, `*/main` dalı  
   - GitHub Webhook: `http://<JENKINS_URL>/github-webhook/`  

5. **CI Test**  
   - Boş commit ile `git push` → Checkout, Build, Test, Archive başarıyla çalıştı  

---

## Karşılaşılan Hatalar & Çözümler
- **`src refspec main does not match any`**  
  _master/main uyuşmazlığı →_  
```bash
git branch -m master main
git push -u origin main
```
Bu, yereldeki ve uzaktaki dal isimleri arasındaki uyumsuzluğu çözer.
