<template>
    <div class="main-wrapper">
        <table class="border-table">
            <tbody class="board-wraaper">
                <tr v-for="(i, y) in chess_board">
                    <td v-for="(j, x) in i">
                        <component :is="j.piece" :data-x="x" :data-y="y" :color="j.color" @pieceClick="pieceClick" :class="[board_color(x,y), effected(x, y, j.effected)]"></component>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import pawn from "./pawn"
import rok from "./rok"
import knight from "./knight"
import queen from "./queen"
import king from "./king"
import bishop from "./bishop"
import empty from "./empty"

export default {
    name : "board",
    components: {pawn, rok, knight, queen, king, bishop, empty},
    data () {
        return {
            chess_board : [[{piece:rok , color : "black", move_count: 0, effected : false },{piece : knight, color : "black", move_count: 0, move_count: 0, effected : false },{piece:bishop, color : "black", move_count: 0, effected : false },{piece:queen, color : "black", move_count: 0, effected : false },{piece:king, color : "black", move_count: 0, effected : false },{piece:bishop, color : "black", move_count: 0, effected : false },{piece:knight, color : "black", move_count: 0, effected : false },{piece:rok, color : "black", move_count: 0, effected : false }]
            ,[{piece:pawn, color : "black", move_count: 0, effected : false },{piece:pawn, color : "black", move_count: 0, effected : false },{piece:pawn, color : "black", move_count: 0, effected : false },{piece:pawn, color : "black", move_count: 0, effected : false },{piece:pawn, color : "black", move_count: 0, effected : false },{piece:pawn, color : "black", move_count: 0, effected : false },{piece:pawn, color : "black", move_count: 0, effected : false },{piece:pawn, color : "black", move_count: 0, effected : false }]
            ,[{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false }]
            ,[{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false }]
            ,[{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false }]
            ,[{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false },{piece:empty, color : "", move_count: 0, effected : false }]
            ,[{piece:pawn, color : "white", move_count: 0, effected : false },{piece:pawn, color : "white", move_count: 0, effected : false },{piece:pawn, color : "white", move_count: 0, effected : false },{piece:pawn, color : "white", move_count: 0, effected : false },{piece:pawn, color : "white", move_count: 0, effected : false },{piece:pawn, color : "white", move_count: 0, effected : false },{piece:pawn, color : "white", move_count: 0, effected : false },{piece:pawn, color : "white", move_count: 0, effected : false }]
            ,[{piece:rok, color : "white", move_count: 0, effected : false },{piece:knight, color : "white", move_count: 0, effected : false },{piece:bishop, color : "white", move_count: 0, effected : false },{piece:queen, color : "white", move_count: 0, effected : false },{piece:king, color : "white", move_count: 0, effected : false },{piece:bishop, color : "white", move_count: 0, effected : false },{piece:knight, color : "white", move_count: 0, effected : false },{piece:rok, color : "white", move_count: 0, effected : false }]],
            turn: 1,
            changed_color : []
        }
    },
    methods : {
        board_color: function(x, y) {
            if((y % 2 == 1 && x % 2 == 1) || (y % 2 == 0 && x % 2 == 0)){
                return "deep-brown"
            }
            else if((y % 2 == 0 && x % 2 == 1) || (y % 2 == 1  && x % 2 == 0)){
                return "light-brown"
            }
        },
        pieceClick: function(piece, x, y){
            if(piece == "rok") {
                if(this.chess_board[x][y].color == "white" && this.turn == 1) {
                    for(var i = x + 1 ; i < 8 ; i++ ) {
                        chess_board[i][y].effected = true;
                        if(this.chess_board[i + 1][y].piece != empty && this.chess_board[i + 1][y].color != "white" && i != 7) {
                            chess_board[i + 1][y].effected = true;
                            break;
                        }
                    }
                    for(var i = x - 1 ; i > -1 ; i-- ) {
                        chess_board[i][y].effected = true;
                        if(this.chess_board[i - 1][y].piece != empty && this.chess_board[i - 1][y].color != "white" && i != 0) {
                            chess_board[i - 1][y].effected = true;
                            break;
                        }
                    }
                    for(var i = y + 1 ; i < 8 ; i++ ) {
                        chess_board[x][i].effected = true;
                        if(this.chess_board[x][i + 1].piece != empty && this.chess_board[x][i + 1].color != "white" && i != 7) {
                            chess_board[x][i + 1].effected = true;
                            break;
                        }
                    }
                    for(var i = y - 1 ; i > -1 ; i-- ) {
                        chess_board[x][i].effected = true;
                        if(this.chess_board[x][i - 1].piece != empty && this.chess_board[x][i - 1].color != "white" && i != 0) {
                            chess_board[x][i - 1].effected = true;
                            break;
                        }
                    }
                }
                else if(this.chess_board[x][y].color == "black" && this.turn == 0) {
                    for(var i = x + 1 ; i < 8 ; i++ ) {
                        chess_board[i][y].effected = true;
                        if(this.chess_board[i + 1][y].piece != empty && this.chess_board[i + 1][y].color != "black" && i != 7) {
                            chess_board[i + 1][y].effected = true;
                            break;
                        }
                    }
                    for(var i = x - 1 ; i > -1 ; i-- ) {
                        chess_board[i][y].effected = true;
                        if(this.chess_board[i - 1][y].piece != empty && this.chess_board[i - 1][y].color != "black" && i != 0) {
                            chess_board[i - 1][y].effected = true;
                            break;
                        }
                    }
                    for(var i = y + 1 ; i < 8 ; i++ ) {
                        chess_board[x][i].effected = true;
                        if(this.chess_board[x][i + 1].piece != empty && this.chess_board[x][i + 1].color != "black" && i != 7) {
                            chess_board[x][i + 1].effected = true;
                            break;
                        }
                    }
                    for(var i = y - 1 ; i > -1 ; i-- ) {
                        chess_board[x][i].effected = true;
                        if(this.chess_board[x][i - 1].piece != empty && this.chess_board[x][i - 1].color != "black" && i != 0) {
                            chess_board[x][i - 1].effected = true;
                            break;
                        }
                    }
                }
            }
            else if(piece == "bishop") {
                if(this.chess_board[x][y].color == "white" && this.turn == 1) {
                    for(var i = x + 1,j = y + 1; i < 8 && j < 8 ; i++, j++ ) {
                        chess_board[i][j].effected = true;
                        if(this.chess_board[i + 1][j + 1].piece != empty && this.chess_board[i + 1][j + 1].color != "white" && i != 7 && j != 7) {
                            chess_board[i + 1][j + 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x - 1,j = y + 1; i > -1 && j < 8 ; i--, j++ ) {
                        chess_board[i][j].effected = true;
                        if(this.chess_board[i - 1][j + 1].piece != empty && this.chess_board[i - 1][j + 1].color != "white" && i != 0 && j != 7) {
                            chess_board[i - 1][j + 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x + 1,j = y - 1; i < 8 && j > -1 ; i++, j-- ) {
                        chess_board[i][j].effected = true;
                        if(this.chess_board[i + 1][j - 1].piece != empty && this.chess_board[i + 1][j - 1].color != "white" && i != 7 && j != 0) {
                            chess_board[i + 1][j - 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x - 1,j = y - 1; i < -1 && j < -1 ; i--, j-- ) {
                        chess_board[i][j].effected = true;
                        if(this.chess_board[i - 1][j - 1].piece != empty && this.chess_board[i - 1][j - 1].color != "white" && i != 0 && j != 0) {
                            chess_board[i - 1][i - 1].effected = true;
                            break;
                        }
                    }
                }
                else if(this.chess_board[x][y].color == "black" && this.turn == 0) {
                    for(var i = x + 1,j = y + 1; i < 8 && j < 8 ; i++, j++ ) {
                        chess_board[i][j].effected = true;
                        if(this.chess_board[i + 1][j + 1].piece != empty && this.chess_board[i + 1][j + 1].color != "black" && i != 7 && j != 7) {
                            chess_board[i + 1][j + 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x - 1,j = y + 1; i > -1 && j < 8 ; i--, j++ ) {
                        chess_board[i][j].effected = true;
                        if(this.chess_board[i - 1][j + 1].piece != empty && this.chess_board[i - 1][j + 1].color != "black" && i != 0 && j != 7) {
                            chess_board[i - 1][j + 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x + 1,j = y - 1; i < 8 && j > -1 ; i++, j-- ) {
                        chess_board[i][j].effected = true;
                        if(this.chess_board[i + 1][j - 1].piece != empty && this.chess_board[i + 1][j - 1].color != "black" && i != 7 && j != 0) {
                            chess_board[i + 1][j - 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x - 1,j = y - 1; i < -1 && j < -1 ; i--, j-- ) {
                        chess_board[i][j].effected = true;
                        if(this.chess_board[i - 1][j - 1].piece != empty && this.chess_board[i - 1][j - 1].color != "black" && i != 0 && j != 0) {
                            chess_board[i - 1][j - 1].effected = true;
                            break;
                        }
                    }
                }
            }
            else if(piece == "king") {
                if(this.chess_board[x][y].color == "white" && this.turn == 1) {
                    if((x + 1) < 8 && (this.chess_board[x + 1][y].piece == empty || this.chess_board[x + 1][y].color != "white"))
                        this.chess_board[x + 1][y].effected = true;
                    if((x - 1) > -1 && (this.chess_board[x - 1][y].piece == empty || this.chess_board[x - 1][y].color != "white"))
                        this.chess_board[x - 1][y].effected = true;
                    if((y + 1) < 8 && (this.chess_board[x][y + 1].piece == empty || this.chess_board[x][y + 1].color != "white"))
                        this.chess_board[x][y + 1].effected = true;
                    if((y - 1) > -1 && (this.chess_board[x][y - 1].piece == empty || this.chess_board[x][y - 1].color != "white"))
                        this.chess_board[x][y - 1].effected = true;
                    if((x + 1) < 8 && (y + 1) < 8 && (this.chess_board[x + 1][y + 1].piece == empty || this.chess_board[x + 1][y + 1].color != "white"))
                        this.chess_board[x + 1][y + 1].effected = true;
                    if((x + 1) < 8 && (y - 1) > -1 && (this.chess_board[x + 1][y - 1].piece == empty || this.chess_board[x + 1][y - 1].color != "white"))
                        this.chess_board[x + 1][y - 1].effected = true;
                    if((x - 1) > -1 && (y + 1) < 8 && (this.chess_board[x - 1][y + 1].piece == empty || this.chess_board[x - 1][y + 1].color != "white"))
                        this.chess_board[x - 1][y + 1].effected = true;
                    if((x - 1) > -1 && (y - 1) > -1 && (this.chess_board[x - 1][y - 1].piece == empty || this.chess_board[x - 1][y - 1].color != "white"))
                        this.chess_board[x - 1][y - 1].effected = true;
                }
                else if(this.chess_board[x][y].color == "black" && this.turn == 0) {
                    if((x + 1) < 8 && (this.chess_board[x + 1][y].piece == empty || this.chess_board[x + 1][y].color != "black"))
                        this.chess_board[x + 1][y].effected = true;
                    if((x - 1) > -1 && (this.chess_board[x - 1][y].piece == empty || this.chess_board[x - 1][y].color != "black"))
                        this.chess_board[x - 1][y].effected = true;
                    if((y + 1) < 8 && (this.chess_board[x][y + 1].piece == empty || this.chess_board[x][y + 1].color != "black"))
                        this.chess_board[x][y + 1].effected = true;
                    if((y - 1) > -1 && (this.chess_board[x][y - 1].piece == empty || this.chess_board[x][y - 1].color != "black"))
                        this.chess_board[x][y - 1].effected = true;
                    if((x + 1) < 8 && (y + 1) < 8 && (this.chess_board[x + 1][y + 1].piece == empty || this.chess_board[x + 1][y + 1].color != "black"))
                        this.chess_board[x + 1][y + 1].effected = true;
                    if((x + 1) < 8 && (y - 1) > -1 && (this.chess_board[x + 1][y - 1].piece == empty || this.chess_board[x + 1][y - 1].color != "black"))
                        this.chess_board[x + 1][y - 1].effected = true;
                    if((x - 1) > -1 && (y + 1) < 8 && (this.chess_board[x - 1][y + 1].piece == empty || this.chess_board[x - 1][y + 1].color != "black"))
                        this.chess_board[x - 1][y + 1].effected = true;
                    if((x - 1) > -1 && (y - 1) > -1 && (this.chess_board[x - 1][y - 1].piece == empty || this.chess_board[x - 1][y - 1].color != "black"))
                        this.chess_board[x - 1][y - 1].effected = true;
                }
            }
            else if(piece == "knight") {
                if(this.chess_board[x][y].color == "white" && this.turn == 1) {
                    if((x + 3) < 8 && (y + 1) < 8 && (this.chess_board[x + 3][y + 1].piece == empty || this.chess_board[x + 3][y + 1].color != "white"))
                        this.chess_board[x + 3][y + 1].effected = true;
                    if((x + 3) < 8 && (y - 1) > -1 && (this.chess_board[x + 3][y - 1].piece == empty || this.chess_board[x + 3][y - 1].color != "white"))
                        this.chess_board[x + 3][y - 1].effected = true;
                    if((x - 3) > -1 && (y + 1) < 8 && (this.chess_board[x - 3][y + 1].piece == empty || this.chess_board[x - 3][y + 1].color != "white"))
                        this.chess_board[x - 3][y + 1].effected = true;
                    if((x - 3) > -1 && (y - 1) > -1 && (this.chess_board[x - 3][y - 1].piece == empty || this.chess_board[x - 3][y - 1].color != "white"))
                        this.chess_board[x - 3][y - 1].effected = true;
                    if((x + 1) < 8 && (y + 3) < 8 && (this.chess_board[x + 1][y + 3].piece == empty || this.chess_board[x + 1][y + 3].color != "white"))
                        this.chess_board[x + 1][y + 3].effected = true;
                    if((x + 1) < 8 && (y - 3) > -1 && (this.chess_board[x + 1][y - 3].piece == empty || this.chess_board[x + 1][y - 3].color != "white"))
                        this.chess_board[x + 1][y + 3].effected = true;
                    if((x - 1) > -1 && (y + 3) < 8 && (this.chess_board[x - 1][y + 3].piece == empty || this.chess_board[x - 1][y - 3].color != "white"))
                        this.chess_board[x + 1][y + 3].effected = true;
                    if((x - 1) > -1 && (y - 3) > -1 && (this.chess_board[x - 1][y - 3].piece == empty || this.chess_board[x - 1][y - 3].color != "white"))
                        this.chess_board[x + 1][y + 3].effected = true;
                }
                else if(this.chess_board[x][y].color == "black" && this.turn == 0) {
                    if((x + 3) < 8 && (y + 1) < 8 && (this.chess_board[x + 3][y + 1].piece == empty || this.chess_board[x + 3][y + 1].color != "black"))
                        this.chess_board[x + 3][y + 1].effected = true;
                    if((x + 3) < 8 && (y - 1) > -1 && (this.chess_board[x + 3][y - 1].piece == empty || this.chess_board[x + 3][y - 1].color != "black"))
                        this.chess_board[x + 3][y - 1].effected = true;
                    if((x - 3) > -1 && (y + 1) < 8 && (this.chess_board[x - 3][y + 1].piece == empty || this.chess_board[x - 3][y + 1].color != "black"))
                        this.chess_board[x - 3][y + 1].effected = true;
                    if((x - 3) > -1 && (y - 1) > -1 && (this.chess_board[x - 3][y - 1].piece == empty || this.chess_board[x - 3][y - 1].color != "black"))
                        this.chess_board[x - 3][y - 1].effected = true;
                    if((x + 1) < 8 && (y + 3) < 8 && (this.chess_board[x + 1][y + 3].piece == empty || this.chess_board[x + 1][y + 3].color != "black"))
                        this.chess_board[x + 1][y + 3].effected = true;
                    if((x + 1) < 8 && (y - 3) > -1 && (this.chess_board[x + 1][y - 3].piece == empty || this.chess_board[x + 1][y - 3].color != "black"))
                        this.chess_board[x + 1][y + 3].effected = true;
                    if((x - 1) > -1 && (y + 3) < 8 && (this.chess_board[x - 1][y + 3].piece == empty || this.chess_board[x - 1][y - 3].color != "black"))
                        this.chess_board[x + 1][y + 3].effected = true;
                    if((x - 1) > -1 && (y - 3) > -1 && (this.chess_board[x - 1][y - 3].piece == empty || this.chess_board[x - 1][y - 3].color != "black"))
                        this.chess_board[x + 1][y + 3].effected = true;
                }
            }
            else if(piece == "pawn") {
                if(this.chess_board[x][y].color == "white" && this.turn == 1) {
                    if((y - 1) > -1 && this.chess_board[x][y - 1].piece == empty) {
                        this.chess_board[x][y - 1].effected = true;
                        if((y - 2) > -1 && this.chess_board[x][y - 2].piece == empty && this.chess_board[x][y].move_count == 0) {
                            this.chess_board[x][y - 2].effected = true;
                        }
                    }
                    if((x - 1) > -1 && (y - 1) > -1 && this.chess_board[x - 1][y - 1].color != "white" && this.chess_board[x - 1][y - 1].piece != empty) {
                        this.chess_board[x - 1][y - 1].effected = true;
                    }
                    if((x + 1) < 8 && (y - 1) > -1 && this.chess_board[x + 1][y - 1].color != "white" && this.chess_board[x + 1][y - 1].piece != empty) {
                        this.chess_board[x + 1][y - 1].effected = true;
                    }
                }
                else if(this.chess_board[x][y].color == "black" && this.turn == 0) {
                    if((y + 1) < 8 && this.chess_board[x][y + 1].piece == empty) {
                        this.chess_board[x][y + 1].effected = true;
                        if((y + 2) < 8 && this.chess_board[x][y + 2].piece == empty && this.chess_board[x][y].move_count == 0) {
                            this.chess_board[x][y + 2].effected = true;
                        }
                    }
                    if((x - 1) > -1 && (y + 1) < 8 && this.chess_board[x - 1][y + 1].color != "black" && this.chess_board[x - 1][y + 1].piece != empty) {
                        this.chess_board[x - 1][y + 1].effected = true;
                    }
                    if((x + 1) < 8 && (y + 1) < 8 && this.chess_board[x + 1][y + 1].color != "black" && this.chess_board[x + 1][y + 1].piece != empty) {
                        this.chess_board[x + 1][y + 1].effected = true;
                    }
                }
            }
            else if(piece == "queen") {
                if(this.chess_board[x][y].color == "white" && this.turn == 1) {
                    for(var i = x + 1 ; i < 7 ; i++) {
                        this.chess_board[i][y].effected = true;
                        if(this.chess_board[i + 1][y].piece != empty && this.chess_board[i + 1][y].color != "white" && i != 7) {
                            this.chess_board[i + 1][y].effected = true;
                            break;
                        }
                    }
                    for(var i = x - 1 ; i > -1 ; i--) {
                        this.chess_board[i][y].effected = true;
                        if(this.chess_board[i - 1][y].piece != empty && this.chess_board[i - 1][y].color != "white" && i != 0) {
                            this.chess_board[i - 1][y].effected = true;
                            break;
                        }
                    }
                    for(var i = y + 1 ; i < 8 ; i++) {
                        this.chess_board[x][i].effected = true;
                        if(this.chess_board[x][i + 1].piece != empty && this.chess_board[x][i + 1].color != "white" && i != 7) {
                            this.chess_board[x][i + 1].effected = true;
                            break;
                        }
                    }
                    for(var i = y - 1 ; i > -1 ; i++) {
                        this.chess_board[x][i].effected = true;
                        if(this.chess_board[x][i - 1].piece != empty &&  this.chess_board[x][i - 1].color != "white" && i != 0) {
                            this.chess_board[x][i - 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x + 1, j = y + 1 ; i < 8 && j < 8 ; i++, j++) {
                        this.chess_board[i][j].effected = true;
                        if(this.chess_board[i + 1][j + 1].piece != empty && this.chess_board[i + 1][j + 1].color != "white" && i != 7 & j != 7) {
                            this.chess_board[i + 1][j + 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x - 1, j = y - 1 ; i > -1 && j > -1 ; i--, j--) {
                        this.chess_board[i][j].effected = true;
                        if(this.chess_board[i - 1][j - 1].piece != empty && this.chess_board[i - 1][j - 1].color != "white" && i != 0 && j != 0) {
                            this.chess_board[i - 1][j - 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x + 1, j = y - 1 ; i < 8 && j > -1 ; i++, j--) {
                        this.chess_board[i][j].effected = true;
                        if(this.chess_board[i + 1][j - 1].piece != empty && this.chess_board[i + 1][j - 1].color != "white" && i != 7 && j != 0) {
                            this.chess_board[i + 1][j - 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x - 1, j = y + 1 ; i > -1 && j < 8 ; i--, j++) {
                        this.chess_board[i][j].effected = true;
                        if(this.chess_board[i - 1][j + 1].piece != empty && this.chess_board[i - 1][j + 1].color != "white" && i != 0 && j != 7) {
                            this.chess_board[i - 1][j + 1].effected = true;
                            break;
                        }
                    }
                }
                else if(this.chess_board[x][y].color == "black" && this.turn == 0) {
                    for(var i = x + 1 ; i < 7 ; i++) {
                        this.chess_board[i][y].effected = true;
                        if(this.chess_board[i + 1][y].piece != empty && this.chess_board[i + 1][y].color != "black" && i != 7) {
                            this.chess_board[i + 1][y].effected = true;
                            break;
                        }
                    }
                    for(var i = x - 1 ; i > -1 ; i--) {
                        this.chess_board[i][y].effected = true;
                        if(this.chess_board[i - 1][y].piece != empty && this.chess_board[i - 1][y].color != "black" && i != 0) {
                            this.chess_board[i - 1][y].effected = true;
                            break;
                        }
                    }
                    for(var i = y + 1 ; i < 8 ; i++) {
                        this.chess_board[x][i].effected = true;
                        if(this.chess_board[x][i + 1].piece != empty && this.chess_board[x][i + 1].color != "black" && i != 7) {
                            this.chess_board[x][i + 1].effected = true;
                            break;
                        }
                    }
                    for(var i = y - 1 ; i > -1 ; i++) {
                        this.chess_board[x][i].effected = true;
                        if(this.chess_board[x][i - 1].piece != empty &&  this.chess_board[x][i - 1].color != "black" && i != 0) {
                            this.chess_board[x][i - 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x + 1, j = y + 1 ; i < 8 && j < 8 ; i++, j++) {
                        this.chess_board[i][j].effected = true;
                        if(this.chess_board[i + 1][j + 1].piece != empty && this.chess_board[i + 1][j + 1].color != "black" && i != 7 & j != 7) {
                            this.chess_board[i + 1][j + 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x - 1, j = y - 1 ; i > -1 && j > -1 ; i--, j--) {
                        this.chess_board[i][j].effected = true;
                        if(this.chess_board[i - 1][j - 1].piece != empty && this.chess_board[i - 1][j - 1].color != "black" && i != 0 && j != 0) {
                            this.chess_board[i - 1][j - 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x + 1, j = y - 1 ; i < 8 && j > -1 ; i++, j--) {
                        this.chess_board[i][j].effected = true;
                        if(this.chess_board[i + 1][j - 1].piece != empty && this.chess_board[i + 1][j - 1].color != "black" && i != 7 && j != 0) {
                            this.chess_board[i + 1][j - 1].effected = true;
                            break;
                        }
                    }
                    for(var i = x - 1, j = y + 1 ; i > -1 && j < 8 ; i--, j++) {
                        this.chess_board[i][j].effected = true;
                        if(this.chess_board[i - 1][j + 1].piece != empty && this.chess_board[i - 1][j + 1].color != "black" && i != 0 && j != 7) {
                            this.chess_board[i - 1][j + 1].effected = true;
                            break;
                        }
                    }
                }
            }
        },
        effected : function(x, y, selected) {
            console.log()
            if(selected){
                this.changed_color.append([x, y])
                return "effected"
            }
            else
                return ""
        }
    }
}
</script>

<style scoped>
.main-wraaper {
    display: flex;
    -webkit-justify-content: center;
    justify-content: center;
    -webkit-align-items: center;
    align-items: center;
}
.border-table {
    border-collapse: collapse;
    border-spacing : 0px 0px;
    
}
.deep-brown {
    background-color: #e6b66c;
}
.light-brown {
    background-color: #6b2a11;
}
.effected {
    background-color: #ac2600;
}
td {
    width: 50px;
    height: 50px;
    margin: 0;
    padding: 0;
}
</style>