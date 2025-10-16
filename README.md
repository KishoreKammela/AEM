# AEM Developer Command Reference

## 🚀 Starting & Stopping AEM

### Start AEM (First Time)
```bash
cd /Users/macbookprom1/Developer/adobe
java -jar aem-author-p4502.jar
```
- Set password to: `admin` / `admin`
- Wait 5-10 minutes for startup

### Start AEM (After Initial Setup)
```bash
cd /Users/macbookprom1/Developer/adobe/crx-quickstart/bin
./start
```

### Stop AEM
```bash
cd /Users/macbookprom1/Developer/adobe/crx-quickstart/bin
./stop
```

### Force Stop AEM
```bash
# Find the process
ps aux | grep java

# Kill it (replace PID with actual process ID)
kill -9 <PID>

# Or kill all Java processes
pkill -9 java
```

---

## 🌐 Access AEM

- **URL:** http://localhost:4502
- **Username:** admin
- **Password:** admin
- **Package Manager:** http://localhost:4502/crx/packmgr/index.jsp
- **CRXDE:** http://localhost:4502/crx/de/index.jsp
- **Web Console:** http://localhost:4502/system/console

---

## 📦 Maven Commands

### Basic Build Commands

#### Build Project (Without Deploy)
```bash
cd /Users/macbookprom1/Developer/adobe/micron
mvn clean install
```

#### Build & Deploy to AEM
```bash
mvn clean install -PautoInstallPackage
```

#### Fast Build & Deploy (Skip Tests & Static Analysis)
```bash
mvn clean install -PautoInstallPackage -DskipTests -PskipStaticAnalysis
```

#### Build Only (No Install)
```bash
mvn clean compile
```

#### Clean Project
```bash
mvn clean
```

---

### Deploy Commands

#### Deploy All Packages
```bash
mvn clean install -PautoInstallPackage
```

#### Deploy ui.apps Module Only
```bash
mvn clean install -PautoInstallPackage -pl ui.apps
```

#### Deploy ui.content Module Only
```bash
mvn clean install -PautoInstallPackage -pl ui.content
```

#### Deploy Core Bundle Only
```bash
mvn clean install -PautoInstallBundle -pl core
```

#### Deploy to Author & Publish
```bash
mvn clean install -PautoInstallPackage,autoInstallPackagePublish
```

#### Deploy with Custom Credentials
```bash
mvn clean install -PautoInstallPackage \
  -Dvault.user=admin \
  -Dvault.password=admin
```

#### Deploy to Custom Port
```bash
mvn clean install -PautoInstallPackage \
  -Daem.port=4502
```

---

### Skip Options

#### Skip Tests
```bash
mvn clean install -DskipTests
```

#### Skip Static Analysis (Checkstyle, PMD, SpotBugs)
```bash
mvn clean install -PskipStaticAnalysis
```

#### Skip Tests + Static Analysis
```bash
mvn clean install -DskipTests -PskipStaticAnalysis
```

#### Skip Integration Tests Only
```bash
mvn clean install -DskipITs
```

#### Skip Unit Tests Only
```bash
mvn clean install -Dtest=false
```

---

### Update & Force Commands

#### Force Update Dependencies
```bash
mvn clean install -U
```

#### Force Update & Deploy
```bash
mvn clean install -U -PautoInstallPackage
```

#### Offline Mode (Use Cached Dependencies)
```bash
mvn clean install -o
```

---

### Specific Module Builds

#### Build Specific Module
```bash
mvn clean install -pl ui.apps
```

#### Build Module & Its Dependencies
```bash
mvn clean install -pl ui.apps -am
```

#### Build Multiple Modules
```bash
mvn clean install -pl ui.apps,core
```

#### Skip Specific Module
```bash
mvn clean install -pl !ui.content
```

---

### Testing Commands

#### Run Tests Only
```bash
mvn test
```

#### Run Specific Test Class
```bash
mvn test -Dtest=MyTestClass
```

#### Run Specific Test Method
```bash
mvn test -Dtest=MyTestClass#myTestMethod
```

#### Run Integration Tests
```bash
mvn verify
```

#### Debug Tests
```bash
mvn test -Dmaven.surefire.debug
```

---

### Package Management

#### Create Package (No Install to AEM)
```bash
mvn clean package
```

#### Create & Install Package Locally
```bash
mvn clean install -PautoInstallPackage
```

#### Build Package with Dependencies
```bash
mvn clean package -PautoInstallPackage
```

---

### Production & Environment Specific

#### Production Build (All Checks)
```bash
mvn clean install
```

#### Development Build (Fast)
```bash
mvn clean install -PautoInstallPackage -DskipTests -PskipStaticAnalysis
```

#### Deploy to Local Author
```bash
mvn clean install -PautoInstallPackage -Daem.host=localhost -Daem.port=4502
```

#### Deploy to Local Publish
```bash
mvn clean install -PautoInstallPackagePublish -Daem.host=localhost -Daem.port=4503
```

#### Deploy to Remote Server
```bash
mvn clean install -PautoInstallPackage \
  -Daem.host=dev-author.example.com \
  -Daem.port=4502 \
  -Dvault.user=admin \
  -Dvault.password=admin
```

---

### Advanced Maven Commands

#### Show Dependency Tree
```bash
mvn dependency:tree
```

#### Check for Dependency Updates
```bash
mvn versions:display-dependency-updates
```

#### Check for Plugin Updates
```bash
mvn versions:display-plugin-updates
```

#### Analyze Dependencies
```bash
mvn dependency:analyze
```

#### Show Effective POM
```bash
mvn help:effective-pom
```

#### List Available Profiles
```bash
mvn help:all-profiles
```

#### Show Active Profiles
```bash
mvn help:active-profiles
```

---

### Debug & Verbose Commands

#### Verbose Output
```bash
mvn clean install -X
```

#### Debug Build Issues
```bash
mvn clean install -X -e
```

#### Show Version Info
```bash
mvn --version
```

---

### Common Combinations

#### Fast Deploy (Most Common for Development)
```bash
mvn clean install -PautoInstallPackage -DskipTests -PskipStaticAnalysis
```

#### Full Build & Deploy (Pre-Commit)
```bash
mvn clean install -PautoInstallPackage
```

#### Quick Module Deploy
```bash
mvn clean install -PautoInstallPackage -pl ui.apps -DskipTests
```

#### Production-Ready Build
```bash
mvn clean install -Dmaven.test.skip=false
```

#### Deploy Everything Fresh
```bash
mvn clean install -U -PautoInstallPackage -DskipTests
```

---

## 📝 Monitoring & Logs

### Watch Error Log (Real-time)
```bash
tail -f /Users/macbookprom1/Developer/adobe/crx-quickstart/logs/error.log
```

### Watch Standard Output
```bash
tail -f /Users/macbookprom1/Developer/adobe/crx-quickstart/logs/stdout.log
```

### Watch Standard Error
```bash
tail -f /Users/macbookprom1/Developer/adobe/crx-quickstart/logs/stderr.log
```

### Check Last 100 Lines of Error Log
```bash
tail -n 100 /Users/macbookprom1/Developer/adobe/crx-quickstart/logs/error.log
```

### Search Logs for Errors
```bash
grep -i "error" /Users/macbookprom1/Developer/adobe/crx-quickstart/logs/error.log
```

---

## 🔄 Reset AEM (Complete Fresh Install)

### Step 1: Stop AEM
```bash
ps aux | grep java
kill -9 <PID>
```

### Step 2: Delete Everything
```bash
cd /Users/macbookprom1/Developer/adobe
sudo rm -rf crx-quickstart
```

### Step 3: Start Fresh
```bash
java -jar aem-author-p4502.jar
```
- Enter password: `admin`
- Re-enter: `admin`

---

## ⚙️ Maven Settings Configuration

### Location
```
~/.m2/settings.xml
```

### Basic AEM Configuration
```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0">
    <servers>
        <server>
            <id>aem-author</id>
            <username>admin</username>
            <password>admin</password>
        </server>
    </servers>
</settings>
```

---

## 🔍 Troubleshooting Commands

### Check if AEM is Running
```bash
ps aux | grep java
```

### Check Port 4502 is in Use
```bash
lsof -i :4502
```

### Check AEM Version
```bash
curl -u admin:admin http://localhost:4502/system/console/status-productinfo.txt
```

### Test Authentication
```bash
curl -u admin:admin http://localhost:4502/crx/packmgr/service.jsp
```

### Check Disk Space
```bash
df -h
```

### Check Memory Usage
```bash
top
# Or
htop
```

---

## 📂 Important AEM Directories

```
/Users/macbookprom1/Developer/adobe/
├── aem-author-p4502.jar          # AEM JAR file
├── crx-quickstart/               # AEM installation
│   ├── app/                      # Application files
│   ├── bin/                      # Start/stop scripts
│   │   ├── start                 # Start script
│   │   └── stop                  # Stop script
│   ├── conf/                     # Configuration files
│   ├── logs/                     # Log files
│   │   ├── error.log
│   │   ├── stdout.log
│   │   └── stderr.log
│   ├── repository/               # Content repository (JCR)
│   └── launchpad/                # OSGi bundles
└── micron/                       # Your AEM project
```

---

## 🛠️ Common Maven Issues & Fixes

### Issue: "Unauthorized" Error
**Fix:** Check credentials in `~/.m2/settings.xml` or pass via command line:
```bash
mvn clean install -PautoInstallPackage -Dvault.user=admin -Dvault.password=admin
```

### Issue: "Connection Refused"
**Fix:** Make sure AEM is running:
```bash
ps aux | grep java
```

### Issue: Package Build Fails
**Fix:** Clean and rebuild:
```bash
mvn clean install -U
```

---

## 📌 Quick Reference

| Task | Command |
|------|---------|
| Start AEM | `./crx-quickstart/bin/start` |
| Stop AEM | `./crx-quickstart/bin/stop` |
| Build & Deploy | `mvn clean install -PautoInstallPackage` |
| Watch Logs | `tail -f crx-quickstart/logs/error.log` |
| Check Running | `ps aux \| grep java` |
| Kill Process | `kill -9 <PID>` |
| Reset AEM | `rm -rf crx-quickstart` |
| Access AEM | http://localhost:4502 |

---

## 💡 Pro Tips

1. **Always monitor logs during startup** to catch issues early
2. **Use `tail -f`** to watch logs in real-time
3. **Keep default credentials** for local development (admin/admin)
4. **Never commit passwords** to version control
5. **Stop AEM properly** before deleting crx-quickstart
6. **First startup takes 5-10 minutes** - be patient!
7. **Use `-U` flag** to force Maven to update dependencies: `mvn clean install -U`

---

## 🔗 Useful URLs

- **AEM Documentation:** https://experienceleague.adobe.com/docs/experience-manager-65.html
- **AEM Developer Docs:** https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html
- **Maven Documentation:** https://maven.apache.org/guides/

---

**Last Updated:** October 16, 2025
