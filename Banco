#include <iostream>
#include <vector>
#include <stdlib.h>
using namespace std;


template<class T>
class no{
  public:
  long long int chave;
  no* direita;
  no* esquerda;
  T dados;
  no(){
    direita=NULL;
    esquerda=NULL;
  }
  no(long long int key, T dado){
    direita=NULL;
    esquerda=NULL;
    chave=key;
    dados=dado;
  }
};

template<class T>
class arvore{
  private: 
  no<T>*raiz;
  
  public:
  arvore(){
    raiz=NULL;
  }
  void insere(long long int chave, T dado){
    insere(raiz,chave,dado);
  }
  void insere(no<T>*aux, long long int chave, T dado){
    if(raiz == NULL){
      raiz = new no<T>(chave, dado);
      return;
    }
    if(chave>aux->chave){
      if(aux->direita==NULL){
        aux->direita = new no<T>(chave, dado);
      return;
      }
      insere(aux->direita,chave,dado);    
    }else{
      if(aux->esquerda==NULL){
        aux->esquerda = new no<T>(chave, dado);
      return;
      }
      insere(aux->esquerda,chave,dado);
    }
    
  }
  void mostra(){
    mostra(raiz);
  }
  void mostra(no<T>* aux){
    if(aux == NULL){
      return;
    }
    mostra (aux->esquerda);
    cout << aux->chave<<"/ ";
    mostra(aux->direita);
  
  }
  bool buscar(long long int chave, T& dado){
    return buscar(raiz,chave,dado);
  }
  bool buscar(no<T>* aux, long long int chave, T& dado){
    if(aux == NULL){
      return false;
    }
    if(aux->chave == chave){
      dado = aux->dados;
      return true;
    }
    if(aux->chave < chave){
      return buscar(aux->direita,chave,dado);
    }
    if(aux->chave > chave){
      return buscar(aux->esquerda,chave,dado);
    }
  }
    bool vazia(){
      return raiz == NULL;
    }
    void percorre(vector<T>& espaco){
      percorre(raiz, espaco);
    }
    void percorre(no<T>*aux,vector<T>& espaco){
        if(aux == NULL){
        return;
    }
      percorre (aux->esquerda, espaco);
      espaco.push_back(aux->dados);
      percorre(aux->direita, espaco);
    }
    void remove(long long int chave){
      raiz=remove(raiz,chave);
    }
    no<T>* MenorValor( no<T>* aux)
{
    no<T>* atual = aux;
 
    while (atual && atual->esquerda != NULL)
        atual = atual->esquerda;
 
    return atual;
}
 

no<T>* remove(no<T>* aux, long long int chave)
{
    if (aux == NULL)
        return aux;

    if (chave < aux->chave)
        aux->esquerda = remove(aux->esquerda, chave);

    else if (chave > aux->chave)
        aux->direita = remove(aux->direita, chave);

    else {

        if (aux->esquerda == NULL) {
            no<T>* temp = aux->direita;
            delete aux;
            return temp;
        }
        else if (aux->direita == NULL) {
            no<T>* temp = aux->direita;
            delete aux;
            return temp;
        }
        no<T>* temp = MenorValor(aux->direita);

        aux->chave = temp->chave;

        aux->direita = remove(aux->direita, temp->chave);
    }
    return aux;
}
};

//Classe Cliente
class Cliente
{
private:
    string agencia;
    string nome;
    string senha;
    string cpf;
    double saldo;
public:
    Cliente(const string agencia,const string nome,const string senha,const string cpf,const double saldo)
    {
        this->agencia = agencia;
        this->nome = nome;
        this->senha = senha;
        this->cpf = cpf;
        this->saldo = saldo;
    }
    Cliente(){

    }

    string getAgencia()
    {
        return agencia;
    }

    string getNome()
    {
        return nome;
    }

    string getSenha()
    {
        return senha;
    }

    void setSenha(const string &senha)
    {
        this->senha = senha;
    }

    string getCPF()
    {
        return cpf;
    }

    double getSaldo()
    {
        return saldo;
    }

    void Deposito(double v)
    {
        this->saldo = this->saldo + v;
    }
    void Saque(const double &v)
    {
        this->saldo = this->saldo - v;
    }
};


//Classe Extrato
class Extrato
{
private:
    string cpf;
    string op;
    double valor;
    double saldo;
public:
    Extrato(const string cpf, const string op, const double valor, const double saldo)
    {
        this->cpf=cpf;
        this->op=op;
        this->valor=valor;
        this->saldo = saldo;
    }
    void setNome(const string &nome)
    {
        this->cpf=nome;
    }
    Extrato(){

    }
    string getCPF()
    {
        return cpf;
    }

    void setOp(const string &op)
    {
        this->op=op;
    }

    string getOp()
    {
        return op;
    }

    void setValor(const double &valor)
    {
        this->valor=valor;
    }

    double getValor()
    {
        return valor;
    }

    double getSaldo()
    {
      return saldo;
    }
};



//Classe Banco: Lista de Clientes / Extratos
class Banco
{
public:
    arvore<Cliente*> L_Clientes; 
    arvore<vector<Extrato>*> Extratos;
    Banco() {
      
    }

    void cadastraCliente(Cliente *C)
    {
      L_Clientes.insere(atoll(C->getCPF().c_str()),C);
    }

    void registraExtrato(Extrato *E)
    {
      vector<Extrato>* aux;
      if(Extratos.buscar(atoll(E->getCPF().c_str()),aux)){
        aux->push_back(*E);
      }else{
        aux=new vector<Extrato>;
        aux->push_back(*E);
        Extratos.insere(atoll(E->getCPF().c_str()),aux);
      }
        delete E;
    }

    void apagaCliente(string cpf)
    {
      apagaExtrato(cpf);
      L_Clientes.remove(atoll(cpf.c_str()));
    }

    void apagaExtrato(string cpf){
      Extratos.remove(atoll(cpf.c_str()));
    }


    void Deposito(string cpf, double valor)
    {
      Cliente* aux;

      if(L_Clientes.buscar(atoll(cpf.c_str()),aux)){
        aux->Deposito(valor); 
      }
    }


    void Saque(string cpf, double valor)
    {
        Cliente* aux;

      if(L_Clientes.buscar(atoll(cpf.c_str()),aux)){
        aux->Saque(valor); 
      }
    }


    void ImprimeExtrato(string cpf){
      Cliente* i;
        vector<Extrato>* aux;
        if(Extratos.buscar(atoll(cpf.c_str()),aux)){
          cout<<"\n";
            cout<<"EXTRATO BANCARIO"<<endl;
            L_Clientes.buscar(atoll(cpf.c_str()),i);
            cout<<"Nome: "<<i->getNome()<<endl;
            cout <<"CPF: " << aux->at(0).getCPF()<<endl;
            cout<<"\n";
          for(Extrato x:*aux){
            cout << "\nOperacao: " << x.getOp() << endl;
            cout << "Valor: R$" << x.getValor() << endl;
            cout<< "Saldo: R$"<<x.getSaldo()<<endl;
          }
          cout<< "Saldo atual: R$"<<i->getSaldo()<<endl;
        }
    }


    void mostraCliente(string cpf)
    {
        Cliente* aux;
        if(L_Clientes.buscar(atoll(cpf.c_str()),aux)){
                cout << "Agencia: " << aux->getAgencia()<<endl;
                cout<<"Nome: " << aux->getNome()<<endl;
                cout<<"CPF: " << aux->getCPF()<<endl;
                cout<<"Saldo Atual: " << aux->getSaldo()<<endl;
                cout<<"Senha: " << aux->getSenha()<<endl;
              }else
        cout<<"Registro de Cliente Nao Encontrado"<<endl;
    }

    void listaClientes()
    {
        vector<Cliente*> aux;
        L_Clientes.percorre(aux);

        for(Cliente* x:aux){
           cout << "Agencia: " << x->getAgencia()<<endl;
            cout << "Nome: " << x->getNome() << endl;
            cout << "CPF: " << x->getCPF() << endl;
            cout << "Saldo Atual: " << x->getSaldo() << endl;
            cout<<"Senha: "<<x->getSenha()<<endl;
            cout<<"\n";

        } 
    }

    void clientesAgencia(string agencia)
    {
       vector<Cliente*> aux;
        L_Clientes.percorre(aux);

        for(Cliente* x:aux){
          if(x->getAgencia()==agencia){
           cout << "Agencia: " << x->getAgencia()<<endl;
            cout << "Nome: " << x->getNome() << endl;
            cout << "CPF: " << x->getCPF() << endl;
            cout << "Saldo Atual: " << x->getSaldo() << endl;
            cout<<"Senha: "<<x->getSenha()<<endl;
            cout<<"\n";
          }

        }
    }

    bool verificaCPF(string cpf)
    {
      Cliente* aux;
      return L_Clientes.buscar(atoll(cpf.c_str()),aux);
    }

    bool verificaSenha(string cpf, string senha){
      Cliente* aux;
      if(L_Clientes.buscar(atoll(cpf.c_str()),aux)){
        return aux->getSenha()==senha;
      }
      return false;
    }

    bool verificaSaque(string cpf, double valor){
      Cliente* aux;
      if(L_Clientes.buscar(atoll(cpf.c_str()),aux)){
        return aux->getSaldo()>=valor;
      }
      return false;
    }

    double pegaSaldo(string cpf){
     
     Cliente* aux;
      if(L_Clientes.buscar(atoll(cpf.c_str()),aux)){
        return aux->getSaldo();
      }
      return -1;
    }
};



int main()
{
    string agencia, nome, cpf;
    string senha;
    double saldo, valor;
    Banco *b = new Banco();
    int op;
    
    cout<<"1-Cadastrar Cliente."<<endl;
    cout<<"2-Realizar Deposito."<<endl;
    cout<<"3-Realizar Saque."<<endl;
    cout<<"4-Mostrar Informacoes de Cliente."<<endl;
    cout<<"5-Mostrar Lista de Clientes do Banco."<<endl;
    cout<<"6-Mostrar Clientes de Uma Determinada Agencia."<<endl;
    cout<<"7-Gerar Extrato de Cliente"<<endl;
    cout<<"8-Apagar Cadastro"<<endl;
    cout<<"0-Sair."<<endl;

    cin>>op;
    while(op!=0)
    {
        switch(op)
        {
          case 1:
          {
              cout<<"Insira da Agencia na Qual e Feita o Cadastro: (5 digitos) ";
              cin>>agencia;
              if(agencia.length()!=5)
              {
                  cout<<"Agencia Invalida"<<endl;
                  break;
              }
              cout<<"Insira o Nome: ";
              cin.ignore();
              getline (cin, nome);
              cout<<"Qual Senha Deseja:(6 digitos) ";
              cin>>senha;
              if(senha.length()!=6)
              {
                  cout<<"Senha Invalida"<<endl;
                  break;
              }
              cout<<"Insira o Numero de CPF:(11 digitos) ";
              cin>>cpf;
              if(cpf.length()!=11)
              {
                  cout<<"CPF Invalido"<<endl;
                  break;
              }
              if(b->verificaCPF(cpf)==true)
              {
                  cout<<"CPF Ja Registrado no Sistema"<<endl;
                  break;
              }
              cout<<"Insira o saldo Inicial Que Deseja: ";
              cin>>saldo;
              if(saldo<0){
                    cout<<"Saldo Invalido"<<endl;
                    break;
              }
              Cliente *c = new Cliente(agencia,nome, senha, cpf, saldo);
              b->cadastraCliente(c);
              cout << endl << "Cadastro realizado com sucesso"<<endl;

              break;
          }

          case 2:
          {
              if(!b->L_Clientes.vazia())
              {
                  cout << "Insira o Seu CPF: ";
                  cin >> cpf;
                  if(!b->verificaCPF(cpf)){
                    cout<<"CPF invalido"<<endl;
                    break;
                  }
                  cout << "Qual Valor Deseja Depositar? ";
                  cin >> valor;
                  if(valor<0){
                    cout<<"Valor Invalido"<<endl;
                    break;
                  }
                  double x = b->pegaSaldo(cpf);
                  b->Deposito(cpf, valor);
                  Extrato *e = new Extrato(cpf, "Deposito", valor, x);
                  b->registraExtrato(e);
                  cout << endl << "Deposito realizado com sucesso"<<endl;
                  getchar();
                  break;
              }
              else
              {
                  cout << "Lista de Clientes Vazia" << endl;
                  getchar();
                  break;
              }
          }

          case 3:
          {
              if(!b->L_Clientes.vazia())
              {
                  cout << "Insira o seu cpf: ";
                  cin >> cpf;
                  if(!b->verificaCPF(cpf)){
                    cout<<"CPF invalido"<<endl;
                    break;
                  }
                  cout << "Digite Sua Senha: ";
                  cin >> senha;
                  if(!b->verificaSenha(cpf, senha)){
                      cout<<"Senha Invalida"<<endl;
                      break;
                  }
                  cout << "Qual Valor Deseja Sacar? ";
                  cin >> valor;
                  if(valor<0){
                    cout<<"Valor Invalido"<<endl;
                    break;
                  }
                  if(!b->verificaSaque(cpf, valor)){
                    cout<<"Saldo Insuficiente"<<endl;
                    break;
                  }
                  double x = b->pegaSaldo(cpf);
                  b->Saque(cpf, valor);
                  Extrato *e1 = new Extrato(cpf, "Saque", valor, x);
                  b->registraExtrato(e1);
                  cout << endl << "Saque realizado com sucesso"<<endl;
                  break;
              }
              else
              {
                  cout << "Lista de Clientes Vazia" << endl;
                  break;
              }
          }

          case 4:
          {
              if(!b->L_Clientes.vazia())
              {
                  cout << "Insira o CPF do Cliente Desejado: ";
                  cin.ignore();
                  getline (cin, nome, '\n');
                  b->mostraCliente(nome);
                  break;
              }
              else
              {
                  cout << "Lista de Clientes Vazia" << endl;
                  break;
              }
          }

          case 5:
          {
              if(!b->L_Clientes.vazia())
              {
                  b->listaClientes();
                  break;
              }
              else
              {
                  cout << "Lista de Clientes Vazia" << endl;
                  break;
              }
          }

          case 6:
          {
              if(!b->L_Clientes.vazia())
              {
                  cout<<"Insira a Agencia na Qual Deseja Ver os Clientes: ";
                  cin>>agencia;
                  b->clientesAgencia(agencia);
                  break;
              }
              else
              {
                  cout << "Lista de Clientes Vazia" << endl;
                  break;
              }
          }

          case 7:
          {
              if(!b->L_Clientes.vazia())
              {
                  cout << "Insira o CPF Para Gerar o Extrato: ";
                  cin >> cpf;
                  if(b->verificaCPF(cpf) == true)
                  {
                    cout << "Insira a Senha: ";
                    cin >> senha;
                    if(b->verificaSenha(cpf, senha)==true){
                      b->ImprimeExtrato(cpf);
                      break;
                    }
                    else{
                      cout << "Senha Incorreta" << endl;
                      break;
                    }
                  }
                  else
                  {
                      cout << "Registro Nao Encontrado" << endl;
                      break;
                  }
              }
              else
              {
                  cout << "Lista de Clientes Vazia" << endl;
                  break;
              }
          }

          case 8:
          {
              if(!b->L_Clientes.vazia())
              {
                cout<<"Insira o CPF do Cliente no Qual Deseja Exluir o Cadastro: ";
                cin>>cpf;
                if(!b->verificaCPF(cpf)){
                  cout<<"Sem Registro de CPF"<<endl;
                  break;
                }
                b->apagaCliente(cpf);
                cout << endl << "Cadastro excluido com sucesso"<<endl;
                break;
              }
              else
              {
                cout << "Lista de Clientes Vazia" << endl;
                break;
              }
              
          }

          default:{
            cout<<"Opcao Invalida"<<endl;
            break;
          }

        }
        /*
        cout << endl<< "Aperte o teclado enter para prosseguir..."<<endl;
        getchar();
        //limpador te tela
        system("clear");
        */
        
        cout<<"\n\n";
        cout<<"1-Cadastrar Cliente."<<endl;
        cout<<"2-Realizar Deposito."<<endl;
        cout<<"3-Realizar Saque."<<endl;
        cout<<"4-Mostrar Informacoes de Cliente."<<endl;
        cout<<"5-Mostrar Lista de Clientes do Banco."<<endl;
        cout<<"6-Mostrar Clientes de Uma Determinada Agencia."<<endl;
        cout<<"7-Gerar Extrato de Cliente"<<endl;
        cout<<"8-Apagar Cadastro"<<endl;
        cout<<"0-Sair."<<endl;
        cout<<"\n\n";

        cin>>op;
    }
    cout<<"Processos Encerrados."<<endl;

    return 0;
}
