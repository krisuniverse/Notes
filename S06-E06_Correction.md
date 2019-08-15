# Les constantes magiques
[Doc Constantes magiques](https://secure.php.net/manual/fr/language.constants.predefined.php)

`__CLASS__` correspond au nom de la classe courante. 
Le nom de la classe contient l'espace de nom dans lequel cette classe a été déclarée.

# La méthode update
```php
/**
* @return LabelModel
*/
    public function update()
    {
        $sql = " SQL
                UPDATE label
                    SET name = :name, updated_at = NOW()
                    WHERE id = :id;
                ";
        $pdo = $this->getDatabaseConnection();
        $request = $pdo->prepare($sql);
        $request->execute(array(
            "name"       => $this->getName(),
            "id"         => $this->getId()
        ));

        return $this;
    }
```