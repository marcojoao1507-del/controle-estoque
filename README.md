# controle-estoque.py
import sqlite3

conn = sqlite3.connect('estoque.db')
cursor = conn.cursor()

cursor.execute('''
    CREATE TABLE IF NOT EXISTS produtos (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        nome TEXT,
        quantidade INTEGER,
        preco REAL
    )
''')
conn.commit()

def cadastrar_produto(nome, qtd, preco):
    cursor.execute("INSERT INTO produtos (nome, quantidade, preco) VALUES (?, ?, ?)", (nome, qtd, preco))
    conn.commit()
    print("✅ Produto cadastrado!")

def listar_produtos():
    cursor.execute("SELECT * FROM produtos")
    produtos = cursor.fetchall()
    if produtos:
        print("\nID | Nome | Qtd | Preço")
        for p in produtos:
            print(f"{p[0]} | {p[1]} | {p[2]} | R$ {p[3]:.2f}")
    else:
        print("Nenhum produto cadastrado.")

# Exemplo de uso
cadastrar_produto("Camisa", 10, 50.0)
cadastrar_produto("Calça", 5, 120.0)
listar_produtos()

conn.close()
