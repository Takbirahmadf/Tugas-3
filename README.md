# Permainan TicTacToe

# Coding dan Penjelasan

    import tkinter as tk
    from tkinter import messagebox

Kode tersebut digunakan untuk mengimport modul tkinter untuk membangun antarmuka pengguna grafis (GUI) dan modul messagebox untuk menampilkan kotak pesan dalam GUI

    # Fungsi untuk mengecek apakah ada pemenang atau seri
    def check_winner():
    for i in range(3):
        if board[i][0] == board[i][1] == board[i][2] != "":
            return board[i][0]
        if board[0][i] == board[1][i] == board[2][i] != "":
            return board[0][i]
    if board[0][0] == board[1][1] == board[2][2] != "":
        return board[0][0]
    if board[0][2] == board[1][1] == board[2][0] != "":
        return board[0][2]
    if all(board[i][j] != "" for i in range(3) for j in range(3)):
        return "Draw"
    
    return None

Fungsi tersebut digunakan untuk mengecek apakah terdapat pemenang ataukah tidak (seri) dalam permainan TicTacToe dengan cara pengecekan baris, kolom, dan diagonal. Jika ada pemenang maka akan mengembalikan "X" atau "O". Jika tidak maka akan mengembalikan none.

    # Fungsi untuk menangani klik pada papan permainan
    winner = None
    turn = True

Variable winner digunakan untuk menyimpan pemenang permainan dan turn digunakan untuk menentukan giliran pemain ( Jika turn adalah True, maka giliran pemain saat ini adalah "X", jika False, giliran pemain saat ini adalah "O").

    def on_click(row, col):
    global turn, winner

    if board[row][col] == "" and not winner:
        if turn:
            board[row][col] = "X"
            buttons[row][col].config(text="X", state="disabled")
        else:
            board[row][col] = "O"
            buttons[row][col].config(text="O", state="disabled")

        turn = not turn

        result = check_winner()
        if result:
            winner = result
            messagebox.showinfo("Tic-Tac-Toe", f"Player {winner} wins!")
            for row in buttons:
                for button in row:
                    button.config(state="disabled")

Fungsi ini memiliki peran penting dalam mengatur interaksi saat pemain mengklik kotak di papan permainan. Dengan cermat, fungsi ini memeriksa apakah kotak yang diklik masih kosong dan juga memastikan bahwa permainan masih berlangsung, sehingga hanya pemain yang sedang giliran yang dapat mengisi kotak tersebut. Setelah mengisi kotak dengan "X" atau "O" sesuai giliran, tombol akan diaktifkan dan dinonaktifkan sesuai peraturan permainan. Setelah tahap ini selesai, langkah selanjutnya adalah memeriksa apakah terdapat seorang pemenang dalam permainan. Untuk melakukannya, fungsi check_winner() akan dipanggil. Jika permainan telah memiliki pemenang, fungsi ini akan menampilkan pesan kemenangan dalam kotak pesan, dan seluruh tombol akan dinonaktifkan dan menyelesaikan permainan.

    # Fungsi untuk me-reset permainan
    def reset_game():
    global board, turn, winner
    board = [["" for _ in range(3)] for _ in range(3)]
    turn = True
    winner = None
    for row in buttons:
        for button in row:
            button.config(text="", state="normal")

Fungsi ini bertugas untuk mengembalikan permainan ke keadaan awal. Dengan menjalankan fungsi ini, semua variabel global akan direset, papan permainan akan dikosongkan, dan tombol-tombol akan kembali ke keadaan awal mereka.

    # Membuat jendela utama
    root = tk.Tk()
    root.title("Tic-Tac-Toe")

Kode ini digunakan untuk membuat jendela utama dengan judul "Tic-Tac-Toe".

    # Membuat papan permainan
    board = [["" for _ in range(3)] for _ in range(3)]
    buttons = [[None for _ in range(3)] for _ in range(3)]
    for i in range(3):
        for j in range(3):
            buttons[i][j] = tk.Button(root, text="", font=("normal", 20), width=5, height=2,
                                 command=lambda i=i, j=j: on_click(i, j))
            buttons[i][j].grid(row=i, column=j)

Kode ini menghasilkan sebuah papan permainan berukuran 3x3 yang terdiri dari tombol-tombol yang dapat diaktifkan dengan klik. Setiap tombol awalnya tidak memiliki teks, dan mereka disesuaikan dengan fungsi on_click() untuk menangani tindakan klik oleh pemain.

    # Membuat tombol reset
    reset_button = tk.Button(root, text="Reset Game", font=("normal", 16), command=reset_game)
    reset_button.grid(row=3, columnspan=3)

Kode ini menghasilkan sebuah tombol yang diberi label "Reset Game" yang akan menjalankan fungsi reset_game() ketika tombol tersebut diklik.

    # Menjalankan GUI
    root.mainloop()

Kode ini memulai eksekusi loop utama dalam antarmuka pengguna (GUI) tkinter, sehingga GUI akan berjalan dan siap menerima input dari pengguna.



Untuk setiap klik di kolom tersebut, klik pertama akan menampilkan "X" dan klik kedua akan menampilkan "O" pada kotak yang dipilih, dan hal ini akan berlangsung hingga terdapat sebaris "X" atau "O" baik secara vertikal, diagonal, atau horizontal yang menentukan hasil permainan. Jika terdapat hasil "X" atau "O" yang sebaris secara vertikal, diagonal, maupun horizontal maka akan muncul hasil permainan yang menunjukkan "Player X wins" atau "Player O wins"

Apabila tombol reset diklik, maka tampilan akan kembali ke kondisi awal
