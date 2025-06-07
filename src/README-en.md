# simple-java-app-pipeline-demo

## Steps Taken

1. **Initial Commit & GitHub Push**  
   - Initialized repo (`git init`), added `pom.xml`, `src/`, `Jenkinsfile`.  
   - Added remote, renamed `master` → `main` to match GitHub’s default branch.

2. **Running Jenkins in Docker**  
   - Pulled LTS image:  
     ```bash
     docker pull jenkins/jenkins:lts
     ```  
   - Started container:  
     ```bash
     docker run -d --name jenkins \
       -p 8080:8080 -p 50000:50000 \
       -v jenkins_home:/var/jenkins_home \
       jenkins/jenkins:lts
     ```  
   - Unlocked Jenkins, installed suggested plugins, created admin user.

3. **Global Tool Configuration**  
   - In **Manage Jenkins → Tools**, added:  
     - **JDK11** (OpenJDK 11, auto-install)  
     - **Maven3** (Apache Maven 3.x, auto-install)

4. **Pipeline Job & Webhook**  
   - Created a Pipeline job that pulls `Jenkinsfile` from SCM on branch `*/main`.  
   - Configured GitHub webhook at `http://<JENKINS_URL>/github-webhook/` to trigger builds on push.

5. **CI Smoke Test**  
   - Made an empty commit and pushed:  
     ```bash
     git commit --allow-empty -m "CI: test webhook"
     git push origin main
     ```  
   - Build ran stages **Checkout → Build → Test → Archive** successfully.

---

## Errors Encountered & How They Were Fixed

- **`src refspec main does not match any`**  
  _Cause:_ Local branch was still `master`, GitHub used `main`.  
  _Fix:_  
```bash
git branch -m master main
git push -u origin main
```
This resolves the mismatch between local and remote branch names.
