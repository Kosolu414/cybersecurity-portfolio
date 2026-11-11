# Scenario A: Bad Password for an Existing Account
net use \\127.0.0.1\c$ "WrongPass123!" /user:"Administrator"

# Scenario B: Unknown / Non-Existent Account
net use \\127.0.0.1\c$ "Password999!" /user:"HackerAccount"
