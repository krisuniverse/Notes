# Static

La méthode getDatabaseConection n'utilise jamais $this, autrement dit l'objet courant n'est pas utile à cette méthode. On peut donc le "fixer" à la classe plutôit qu'à l'instance. On va donc utiliser le mot clé `static`.

Static, c'est la classe courante, si tu apelle avec une classe A, une méthode qui est dans une classe B, tu récupère avec static, la classe A

Une méthode statique n'a pas besoin d'être instanciée pour avoir accès à ses méthodes