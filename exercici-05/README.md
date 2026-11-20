# Exercici 5: top_k i top_p (ampliació)

**Objectiu:** veure com limitem els candidats entre els quals el model tria el token següent.

**Predicció (abans de començar):** què creieu que passarà si el model només pot triar entre 1 candidat? I si pot triar entre tots?

**La vostra predicció:**

- `top_k`: només es consideren els *k* tokens més probables.
- `top_p`: només es consideren els tokens més probables fins a sumar aquesta probabilitat.

1. **Actualitzeu `lab.py`:** afegiu les opcions `--top_k`, `--top_p` i `--num_predict`. Van dins d'`options` i només s'han d'enviar si s'indiquen. `--num_predict` és el nombre màxim de tokens de la resposta: aquí només el necessiteu perquè les respostes de la configuració E no s'allarguin sense fi; a l'exercici 6 el treballareu a fons. **Comproveu** que l'script imprimeix les opcions que li passeu: `python lab.py "Hola" --vegades 1 --temperature 0 --seed 1 --top_k 5 --top_p 0.9 --num_predict 10` ha de mostrar entre les opcions `seed`, `top_k`, `top_p` i `num_predict`.
2. Deseu aquest prompt en una variable de PowerShell:

   ```powershell
   $prompt = "Completa la frase: «Si funciona, no ho toquis, perquè…». Respon només amb el final de la frase, en 10 paraules com a màxim."
   ```

3. Per a cada fila de la taula, executeu l'ordre corresponent (3 repeticions, temperatura 1 i sense llavor, així cada repetició pot donar un resultat diferent):

   ```powershell
   # Configuració A
   python lab.py $prompt --vegades 3 --temperature 1 --top_k 1 --top_p 0.9 --num_predict 40
   # Configuració B
   python lab.py $prompt --vegades 3 --temperature 1 --top_k 100 --top_p 0.1 --num_predict 40
   # Configuració C
   python lab.py $prompt --vegades 3 --temperature 1 --top_k 100 --top_p 1.0 --num_predict 40
   # Configuració D (temperatura 2.5 amb els filtres per defecte)
   python lab.py $prompt --vegades 3 --temperature 2.5 --top_k 64 --top_p 0.95 --num_predict 40
   # Configuració E (temperatura 2.5 sense filtres: top_k 0 i top_p 1)
   python lab.py $prompt --vegades 3 --temperature 2.5 --top_k 0 --top_p 1 --num_predict 40
   ```

| Configuració | top_k | top_p | Observacions |
| :- | :- | :- | :- |
| A | 1 | 0.9 | |
| B | 100 | 0.1 | |
| C | 100 | 1.0 | |
| D (temperatura 2.5) | 64 | 0.95 | |
| E (temperatura 2.5) | 0 | 1 | |

## Preguntes

1. Quina configuració es comporta com si la temperatura fos 0? Per què?

   **Resposta:**

2. Quina té menys varietat entre repeticions: B o C? Expliqueu-ho.

   **Resposta:**

3. Compareu les configuracions D i E. Per què `top_k` i `top_p` ajuden a evitar respostes sense sentit quan la temperatura és alta?

   **Resposta:**

