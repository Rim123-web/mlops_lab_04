

<div class="lab-section">

<h2>Lab 4 — Versionnement du projet avec Git</h2>

<h3>Étape 1 : Créer le dépôt GitHub et connecter le remote</h3>

<p>
Cette étape consiste à créer un dépôt GitHub pour le projet et à connecter votre dépôt local avec
le remote afin de pouvoir synchroniser le code.
</p>

<h3> Instructions</h3>

<ul>
    <li>Aller sur GitHub → New Repository → nom : <code>mlops-lab-01</code></li>
    <img width="661" height="374" alt="img1_cd" src="https://github.com/user-attachments/assets/cf6761d2-503e-41a8-91e0-90324debc607" />

 <li>Copier l’URL HTTPS du dépôt créé</li>
    <li>Connecter le dépôt local au remote :</li>
    
</ul>

<pre><code>git remote add origin https://github.com/&lt;USER&gt;/mlops-lab-01.git
git branch -M main
git push -u origin main</code></pre>

<img width="332" height="212" alt="img2_cd" src="https://github.com/user-attachments/assets/6ea31a66-940d-498f-abce-1e54b82eeb45" />

<!-- ================== LAB 1 - STEP 2 ================== -->


<div class="lab-section">


<h3>Étape 2 : Définir les secrets GitHub</h3>

<p>
Cette étape permet de sécuriser certaines variables et secrets utilisés par le workflow CI/CD
dans GitHub Actions. Les secrets sont stockés de manière sécurisée et ne sont pas visibles publiquement.
</p>

<h3> Instructions</h3>

<ul>
    <li>Aller dans : <strong>GitHub → Repository → Settings → Secrets and Variables → Actions → New repository secret</strong></li>
    <img width="237" height="192" alt="img3_cd" src="https://github.com/user-attachments/assets/a23b6539-40e0-430d-9b42-4e9af69fd385" />

  <li>Créer les secrets et variables suivantes :</li>
</ul>

<pre><code># Variables pour GitHub Actions
PY_VERSION = 3.10
F1_GATE_THRESHOLD = 0.70
APP_ENV = staging

# Secret sécurisé
DEMO_SECRET = "CI/CD demo secret for students"</code></pre>

<img width="685" height="332" alt="img4_cd" src="https://github.com/user-attachments/assets/80712b73-6d9e-438d-943b-2ff5fe6a2eca" />

<img width="605" height="125" alt="img5_cd" src="https://github.com/user-attachments/assets/5d9b29e8-15d6-41d8-b5e2-a319a9143334" />

<img width="625" height="235" alt="img6_cd" src="https://github.com/user-attachments/assets/9685b27a-df44-44c1-8adf-c108f95edef4" />


</div>
<!-- ================== END LAB 1 - STEP 2 ================== -->

</div>
<!-- ================== END LAB 1 - STEP 1 ================== -->


<!-- ================== LAB 1 - STEP 3 ================== -->


<div class="lab-section">


<h3>Étape 3 : Création du workflow CI/CD GitHub Actions</h3>

<p>
Dans cette étape, nous créons un workflow CI/CD pour automatiser le processus ML. 
Le workflow se déclenche sur les <strong>push</strong> et <strong>pull requests</strong> sur la branche <code>main</code>.
Il comprend deux jobs principaux : <code>ci</code> (intégration continue) et <code>cd</code> (déploiement simulé).
</p>

<h3>📌 Instructions et fonctionnalités</h3>

<ul>
    <li>Job <strong>CI</strong> : </li>
    <ul>
        <li>Checkout du code avec <code>actions/checkout@v4</code></li>
        <li>Installation de Python (<code>${{ vars.PY_VERSION }}</code>)</li>
        <li>Mise en cache des dépendances pip et de DVC</li>
        <li>Exécution de <code>generate_data.py</code> pour créer les données brutes</li>
        <li>Exécution du pipeline DVC via <code>dvc repro</code></li>
        <li>Vérification des métriques (Quality Gate F1)</li>
        <li>Upload des artefacts ML (models, registry, reports)</li>
    </ul>
    <li>Job <strong>CD</strong> (simulé) : </li>
    <ul>
        <li>Se déclenche uniquement sur <code>main</code></li>
        <li>Télécharge les artefacts validés du job CI</li>
        <li>Simulation d’un déploiement SSH avec affichage des artefacts et variables d’environnement</li>
    </ul>
</ul>
<img width="673" height="402" alt="img7_cd" src="https://github.com/user-attachments/assets/9f039fd0-53a2-45d3-87b8-be66c3df1655" />




</div>
<!-- ================== END LAB 1 - STEP 3 ================== -->


<!-- ================== LAB 1 - STEP 4 ================== -->


<div class="lab-section">


<h3>Étape 4 : Commit et push</h3>

<p>
Cette étape consiste à vérifier que les modifications locales sont correctement commit et poussées sur GitHub, 
et que le workflow CI/CD s’exécute automatiquement.
</p>

<h3>Instructions</h3>

<ul>
    <li>Effectuer un commit des changements locaux :</li>
</ul>

<pre><code>git add .
git commit -m "Ajout du workflow CI/CD et des secrets"
git push origin main</code></pre>

<ul>
    <li>Aller sur GitHub → Repository → Actions pour vérifier l’exécution du workflow</li>
    <li>Vérifier :</li>
</ul>

<img width="479" height="77" alt="img8_cd" src="https://github.com/user-attachments/assets/8304c971-e3b2-454f-92ac-1dcd1600b666" />


<pre><code>job ci   → doit installer Python, exécuter les scripts et uploader les artefacts
job cd   → doit se déclencher uniquement sur main et simuler le déploiement SSH</code></pre>


<!-- ================== END LAB 1 - STEP 4 ================== -->
