class Utilisateur:
    def __init__(self, nom, prenom, credit=0):
        self.nom = nom
        self.prenom = prenom
        self.credit = credit

class Ordinateur:
    def __init__(self, numero, disponible=True):
        self.numero = numero
        self.disponible = disponible

class Cyber:
    def __init__(self):
        self.utilisateurs = []
        self.ordinateurs = [Ordinateur(numero) for numero in range(1, 11)]  # 10 ordinateurs par défaut

    def inscription_utilisateur(self, nom, prenom):
        utilisateur = Utilisateur(nom, prenom)
        self.utilisateurs.append(utilisateur)
        print(f"{prenom} {nom} a été inscrit avec succès.")

    def afficher_ordinateurs_disponibles(self):
        print("Ordinateurs disponibles :")
        for ordinateur in self.ordinateurs:
            if ordinateur.disponible:
                print(f"Ordinateur {ordinateur.numero}")

    def reserver_ordinateur(self, utilisateur, numero_ordinateur, duree):
        ordinateur = self.ordinateurs[numero_ordinateur - 1]
        if ordinateur.disponible:
            if utilisateur.credit >= duree:
                utilisateur.credit -= duree
                ordinateur.disponible = False
                print(f"{utilisateur.prenom} {utilisateur.nom} a réservé l'ordinateur {ordinateur.numero} pour {duree} heures.")
            else:
                print("Crédit insuffisant pour réserver cet ordinateur.")
        else:
            print(f"L'ordinateur {ordinateur.numero} est déjà réservé.")

    def recharger_credit(self, utilisateur, montant):
        utilisateur.credit += montant
        print(f"Crédit de {utilisateur.prenom} {utilisateur.nom} rechargé avec succès. Nouveau solde : {utilisateur.credit}.")

# Exemple d'utilisation de l'application
cyber = Cyber()
cyber.inscription_utilisateur("Doe", "John")
cyber.recharger_credit(cyber.utilisateurs[0], 50)
cyber.afficher_ordinateurs_disponibles()
cyber.reserver_ordinateur(cyber.utilisateurs[0], 1, 2)
