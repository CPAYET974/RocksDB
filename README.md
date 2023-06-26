## Installation de RocksDB

Suivez ces étapes pour installer RocksDB sur votre système :

**1. Prérequis**

Assurez-vous d'avoir les éléments suivants installés sur votre système :

- Un compilateur C++ compatible avec C++11 (par exemple, GCC version 4.8 ou supérieure)
- CMake version 2.8.12.2 ou supérieure
- Git

**2. Récupération du code source**

Clonez le référentiel RocksDB depuis GitHub en exécutant la commande suivante :

```
git clone https://github.com/facebook/rocksdb.git
```

**3. Construction de RocksDB**

Accédez au répertoire cloné :

```
cd rocksdb
```

Générez les fichiers de construction en utilisant CMake :

```
mkdir build && cd build
cmake ..
```

Construisez RocksDB en exécutant la commande make :

```
make -j4
```

Cela lancera le processus de compilation et de construction de RocksDB. L'option `-j4` spécifie le nombre de threads à utiliser pour la compilation (vous pouvez ajuster ce nombre en fonction de votre système).

**4. Installation de RocksDB **

Pour installer RocksDB sur votre système, exécutez la commande suivante :

```
sudo make install
```

Cela copiera les fichiers de bibliothèque, les en-têtes et les binaires nécessaires dans les emplacements système appropriés.

**5. Utilisation de RocksDB**

Voici un exemple simple d'utilisation de RocksDB dans votre code C++ :

```cpp
#include <iostream>
#include <rocksdb/db.h>

int main() {
  rocksdb::DB* db;
  rocksdb::Options options;
  options.create_if_missing = true;

  rocksdb::Status status = rocksdb::DB::Open(options, "/path/to/db", &db);
  if (status.ok()) {
    std::string key = "my_key";
    std::string value = "my_value";

    // Écriture d'une paire clé-valeur
    status = db->Put(rocksdb::WriteOptions(), key, value);
    if (status.ok()) {
      // Lecture de la valeur en utilisant la clé
      std::string result;
      status = db->Get(rocksdb::ReadOptions(), key, &result);
      if (status.ok()) {
        std::cout << "Valeur de la clé : " << result << std::endl;
      } else {
        std::cerr << "Erreur lors de la lecture de la valeur : " << status.ToString() << std::endl;
      }
    } else {
      std::cerr << "Erreur lors de l'écriture de la paire clé-valeur : " << status.ToString() << std::endl;
    }

    delete db;
  } else {
    std::cerr << "Erreur lors de l'ouverture de la base de données : " << status.ToString() << std::endl;
  }

  return 0;
}
```

Assurez-vous d'inclure les en-têtes de RocksDB et de lier votre application avec les bibliothèques de RocksDB lors de la compilation.
