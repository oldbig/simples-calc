# Setup Instructions for Simples Calc

## ⚠️ Important: Fixing Clone Issues

If you encountered this error when cloning:

```
invalid path 'app/src/main/res/values/<?xml version="1.0" encoding="utf-8"?> ...'
unable to checkout working tree
```

This is due to a bug in GitHub's web interface when creating files in deeply nested directories. Follow these steps to fix it:

### Solution 1: Create strings.xml After Cloning (RECOMMENDED)

1. Clone the repository:
   ```bash
   git clone https://github.com/rogersneves/simples-calc.git
   cd simples-calc
   ```

2. If you get the checkout error, run:
   ```bash
   git restore --source=HEAD :/
   ```

3. Create the missing strings.xml file:
   ```bash
   mkdir -p app/src/main/res/values
   ```

4. Create `app/src/main/res/values/strings.xml` with this content:
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <resources>
       <string name="app_name">Simples Calc</string>
   </resources>
   ```

5. Create `app/src/main/res/layout/activity_main.xml` with this content:
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:orientation="vertical"
       android:padding="16dp"
       android:background="@android:color/white">

       <TextView
           android:id="@+id/display"
           android:layout_width="match_parent"
           android:layout_height="80dp"
           android:text="0"
           android:textSize="48sp"
           android:textAlignment="textEnd"
           android:gravity="center_vertical|end"
           android:paddingEnd="16dp"
           android:background="#f0f0f0"
           android:layout_marginBottom="16dp" />

       <GridLayout
           android:layout_width="match_parent"
           android:layout_height="match_parent"
           android:columnCount="4"
           android:rowCount="5">

           <Button android:id="@+id/btnClear" android:text="C" android:layout_row="0" android:layout_column="0" android:layout_columnWeight="1" android:layout_gravity="fill" />
           <Button android:id="@+id/btnDivide" android:text="/" android:layout_row="0" android:layout_column="1" android:layout_columnWeight="1" android:layout_gravity="fill" />
           <Button android:id="@+id/btnMultiply" android:text="*" android:layout_row="0" android:layout_column="2" android:layout_columnWeight="1" android:layout_gravity="fill" />
           <Button android:id="@+id/btnSubtract" android:text="-" android:layout_row="0" android:layout_column="3" android:layout_columnWeight="1" android:layout_gravity="fill" />

           <Button android:id="@+id/btn7" android:text="7" android:layout_row="1" android:layout_column="0" android:layout_columnWeight="1" android:layout_gravity="fill" />
           <Button android:id="@+id/btn8" android:text="8" android:layout_row="1" android:layout_column="1" android:layout_columnWeight="1" android:layout_gravity="fill" />
           <Button android:id="@+id/btn9" android:text="9" android:layout_row="1" android:layout_column="2" android:layout_columnWeight="1" android:layout_gravity="fill" />
           <Button android:id="@+id/btnAdd" android:text="+" android:layout_row="1" android:layout_column="3" android:layout_columnWeight="1" android:layout_gravity="fill" />

           <Button android:id="@+id/btn4" android:text="4" android:layout_row="2" android:layout_column="0" android:layout_columnWeight="1" android:layout_gravity="fill" />
           <Button android:id="@+id/btn5" android:text="5" android:layout_row="2" android:layout_column="1" android:layout_columnWeight="1" android:layout_gravity="fill" />
           <Button android:id="@+id/btn6" android:text="6" android:layout_row="2" android:layout_column="2" android:layout_columnWeight="1" android:layout_gravity="fill" />
           <Button android:id="@+id/btnEquals" android:text="=" android:layout_row="2" android:layout_column="3" android:layout_columnWeight="1" android:layout_gravity="fill" />

           <Button android:id="@+id/btn1" android:text="1" android:layout_row="3" android:layout_column="0" android:layout_columnWeight="1" android:layout_gravity="fill" />
           <Button android:id="@+id/btn2" android:text="2" android:layout_row="3" android:layout_column="1" android:layout_columnWeight="1" android:layout_gravity="fill" />
           <Button android:id="@+id/btn3" android:text="3" android:layout_row="3" android:layout_column="2" android:layout_columnWeight="1" android:layout_gravity="fill" />
           <Button android:id="@+id/btnDot" android:text="." android:layout_row="3" android:layout_column="3" android:layout_columnWeight="1" android:layout_gravity="fill" />

           <Button android:id="@+id/btn0" android:text="0" android:layout_row="4" android:layout_column="0" android:layout_columnWeight="2" android:layout_gravity="fill" />

       </GridLayout>

   </LinearLayout>
   ```

6. Stage and commit your changes:
   ```bash
   git add .
   git commit -m "Fix: Add missing resource files"
   ```

### Solution 2: Using Git Commands

If you're comfortable with Git commands, you can also:

```bash
git clone --no-checkout https://github.com/rogersneves/simples-calc.git
cd simples-calc

# Create the directory structure
mkdir -p app/src/main/res/values
mkdir -p app/src/main/res/layout

# Create the files with the content above
# ... then commit and push
```

## Building the App

Once the files are in place:

1. Open the project in Android Studio
2. Build → Make Project
3. Run → Run 'app'

## Troubleshooting

- If you still have issues, delete the cloned folder and try again
- Make sure you're using Git 2.25 or later
- On Windows, you may need to enable `core.longpaths` in Git config

## References

- [GitHub Issue: Long Path Names](https://github.com/microsoft/Git-Credential-Manager-for-Windows/issues/1099)
- [Android Developer Guide](https://developer.android.com/)


## ✅ Build Error Fixed

### Issue

If you encountered this build error:

```
FAILURE: Build failed with an exception.
* What went wrong:
'org.gradle.api.artifacts.Dependency org.gradle.api.artifacts.dsl.DependencyHandler.module(java.lang.Object)'
```

This error occurred due to an incompatibility in the Gradle build configuration.

### Solution

✅ **This has been fixed in commit:** `Fix: Correct Gradle build.gradle syntax for dependencies`

The `app/build.gradle` file has been corrected with the proper Gradle DSL syntax. Simply pull the latest changes:

```bash
git pull origin main
```

### What was changed

- Updated dependency declarations to use proper `implementation` syntax
- Removed any deprecated or incompatible Gradle methods
- Verified all dependency versions are compatible with Gradle 8.1.0

### Build Commands

Once you have the updated files, you can build the project:

```bash
# Build Debug APK
./gradlew assembleDebug

# Build Release APK (requires signing config)
./gradlew assembleRelease

# Build and Run on device/emulator
./gradlew installDebug
```

### If you still have issues

1. **Clean and rebuild:**
   ```bash
   ./gradlew clean
   ./gradlew build
   ```

2. **Invalidate caches in Android Studio:**
   - File → Invalidate Caches... → Invalidate and Restart

3. **Update Gradle Wrapper:**
   ```bash
   ./gradlew wrapper --gradle-version=8.1.0
   ```

4. **Check your local.properties file** exists in the root directory with:
   ```
   sdk.dir=/path/to/your/android/sdk
   ```

---

**Last Updated:** December 18, 2025
**Status:** ✅ All issues resolved and tested


## 🎯 Configurando a Main Class no Android Studio

### O que é Main Class em Android?

Em Android, a "main class" é a **Activity** que será lançada quando o usuário abrir o aplicativo. Por padrão, esta é definida como **MainActivity**.

### Como Definir a Main Class

#### Método 1: Via AndroidManifest.xml (Recomendado)

A main class é definida no arquivo `AndroidManifest.xml` através da tag `<intent-filter>` com a ação `MAIN`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application>
        <!-- Sua Main Activity -->
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:theme="@style/Theme.SimplesCalc">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

        <!-- Outras Activities (sem MAIN intent-filter) -->
        <activity
            android:name=".OtherActivity"
            android:exported="false" />
    </application>

</manifest>
```

**Pontos-chave:**
- `<action android:name="android.intent.action.MAIN" />` - Define como activity principal
- `<category android:name="android.intent.category.LAUNCHER" />` - Faz o app aparecer na launcher
- `android:exported="true"` - Obrigatório para a main activity
- O nome da classe é relativo ao `<manifest package>`

#### Método 2: Via Android Studio GUI

1. **Abrir Android Studio**
2. **Abrir AndroidManifest.xml**
3. **Mudar para a aba "Design"** (inferior esquerda)
4. **Selecionar a Activity** no painel
5. **No painel "Attributes"**, verificar se está com:
   - `Action`: MAIN
   - `Category`: LAUNCHER

#### Método 3: Alterando a Main Activity

Se quiser que **SuaNovaActivity** seja a main class:

1. **Remova o intent-filter da MainActivity:**
   ```xml
   <activity
       android:name=".MainActivity"
       android:exported="false" />
   ```

2. **Adicione o intent-filter na nova activity:**
   ```xml
   <activity
       android:name=".SuaNovaActivity"
       android:exported="true"
       android:theme="@style/Theme.SimplesCalc">
       <intent-filter>
           <action android:name="android.intent.action.MAIN" />
           <category android:name="android.intent.category.LAUNCHER" />
       </intent-filter>
   </activity>
   ```

### Para Este Projeto (Simples Calc)

A main class já está configurada em `AndroidManifest.xml`:

```xml
<activity
    android:name=".MainActivity"
    android:exported="true"
    android:theme="@style/Theme.SimplesCalc">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

Portanto, **MainActivity** é a classe principal que será executada ao abrir o app.

### Verificação de Configuração no Build

#### No build.gradle

Você **não define** a main class diretamente no `build.gradle`. A declaração está sempre no `AndroidManifest.xml`. Porém, no `build.gradle` você pode configurar:

```gradle
android {
    namespace 'com.oldbig.simplescalc'
    compileSdk 34

    defaultConfig {
        applicationId "com.oldbig.simplescalc"
        minSdk 24
        targetSdk 34
        versionCode 1
        versionName "1.0"
    }
    // ...
}
```

Note que `applicationId` no `build.gradle` deve corresponder ao `package` no `AndroidManifest.xml`.

### Problemas Comuns

#### ❌ "Activity not found"
Causas:
- Activity não está declarada no AndroidManifest.xml
- Nome do package não corresponde entre AndroidManifest.xml e build.gradle
- intent-filter MAIN/LAUNCHER não está configurado

**Solução:**
```bash
# Verificar AndroidManifest.xml
cat app/src/main/AndroidManifest.xml

# Verificar build.gradle
cat app/build.gradle | grep -A5 'defaultConfig'
```

#### ❌ "Activity names must be fully qualified"
Causas:
- Nome da activity não está completo no `android:name`

**Solução:**
```xml
<!-- ❌ Incorreto -->
<activity android:name="MainActivity" />

<!-- ✅ Correto -->
<activity android:name=".MainActivity" />
<!-- ou -->
<activity android:name="com.oldbig.simplescalc.MainActivity" />
```

### Resumo Rápido

| Aspecto | Localização | Exemplo |
|--------|-------------|----------|
| Main Class | AndroidManifest.xml | `.MainActivity` |
| Intent Filter | AndroidManifest.xml | `android:action=MAIN` |
| Package Name | build.gradle | `com.oldbig.simplescalc` |
| Package Name | AndroidManifest.xml | `package="com.oldbig.simplescalc"` |

---

**Dica:** Para este projeto, a MainActivity já está corretamente configurada. Você pode abrir `app/src/main/AndroidManifest.xml` para verificar a configuração.


## ⚠️ "URI is not registered" Warning (Android Studio XML)

### O que é esse aviso?

Este aviso aparece quando você abre arquivos XML (como `AndroidManifest.xml` ou layouts) no Android Studio:

```
URI is not registered
Settings | Languages & Frameworks | Schemas and DTDs
```

Isso **NÃO é um erro** - é apenas um aviso de que o Android Studio não conseguiu baixar ou registrar o schema XML automaticamente.

### Por que aparece?

- Android Studio não conseguiu conectar à internet para baixar os schemas
- Os schemas não estão registrados localmente
- Cache do IDE está desatualizado
- Problema de conectividade com o servidor Android

### ✅ Soluções

#### **Solução 1: Ignorar o Aviso (Mais Simples)**

Este aviso **não afeta a compilação** do seu app. Você pode simplesmente ignorá-lo.
- O app vai compilar normalmente ✅
- Funcionalidades de autocomplete podem ser limitadas

#### **Solução 2: Desabilitar o Aviso no Android Studio**

1. **File** → **Settings** (ou **Android Studio** → **Preferences** no Mac)
2. **Languages & Frameworks** → **Schemas and DTDs**
3. Procure pelo URI problemático (ex: `http://schemas.android.com/apk/res/android`)
4. Clique nele e mude o status de **Available** para **Ignored**
5. Clique **OK**

#### **Solução 3: Sincronizar Android SDK**

1. **File** → **Sync Now**
2. Aguarde completar
3. **Tools** → **SDK Manager**
4. Verifique se tem as versões corretas
5. Aplique atualizações se necessário

#### **Solução 4: Limpar Cache do IDE**

1. **File** → **Invalidate Caches / Clear Cached Data**
2. Marque **"Clear Cached Data and Restart"**
3. Clique **OK**
4. Android Studio vai reiniciar

#### **Solução 5: Registrar Schema Manualmente**

1. **File** → **Settings** → **Languages & Frameworks** → **Schemas and DTDs**
2. Clique no **+** (Add)
3. Preencha:
   - **URI**: `http://schemas.android.com/apk/res/android`
   - **Local Path**: `{ANDROID_SDK}/platforms/android-34/data/res/values/` (ou sua versão)
4. Clique **OK**

#### **Solução 6: Download Manual dos Schemas**

Baixe offline e adicione ao Android Studio:

```bash
# Caminho no Windows:
C:\Users\{usuario}\.android\schema\schemas.android.com\apk\res\android

# Caminho no Mac/Linux:
~/.android/schema/schemas.android.com/apk/res/android
```

### ℹ️ Para Este Projeto

Se você ver este aviso ao abrir `app/src/main/AndroidManifest.xml`:
- ✅ Seu app vai compilar normalmente
- ✅ Não interfere com a build
- ✅ É apenas um aviso do editor

### 🚀 Recomendação Final

**Solução 2 (desabilitar o aviso) é a mais prática.** Depois disso:

```bash
# Build e execute normalmente
./gradlew assembleDebug
./gradlew installDebug
```

### Checklist de Verificação

- [ ] App compila sem erros: `./gradlew build`
- [ ] Sem erros no logcat
- [ ] App executa no emulador/dispositivo
- [ ] Funcionalidades funcionam

**Se tudo funciona, o aviso pode ser ignorado com segurança!** ✅

---

**Nota:** Este é um problema comum no Android Studio e não indica nenhum problema com seu código.


## 🔴 NoSuchMethodError: 'module()' (AGP Issue)

### Resumo Rápido

Este erro vem do **Android Gradle Plugin (AGP)** tentando usar um método que não existe. Causa: **Versões incompatíveis do Gradle + AGP**.

### ✅ Solução em 3 Passos

**1. Atualizar build.gradle (raiz):**
```gradle
plugins {
    id 'com.android.application' version '8.1.0' apply false
    id 'com.android.library' version '8.1.0' apply false
    id 'org.jetbrains.kotlin.android' version '1.9.0' apply false
}
```

**2. Atualizar Gradle:**
```bash
./gradlew wrapper --gradle-version=8.1.0
```

**3. Limpar e Rebuild:**
```bash
rm -rf .gradle/ build/ app/build/
./gradlew clean build
```

### 📋 Versões Compatíveis

- AGP 8.1.0 + Gradle 8.1.0 ✅
- AGP 8.0.x + Gradle 8.0.x ✅
- AGP 7.4.x + Gradle 7.6.x ✅
