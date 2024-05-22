<?php

/*Classe para representar o paciente */
class Paciente {
    protected $nome;
    protected $idade;
    protected $sexo;
    protected $historico;
    protected $consultas;
    protected $medicoResponsavel;

    public function __construct($nome, $idade, $sexo) {
        $this->nome = $nome;
        $this->idade = $idade;
        $this->sexo = $sexo;
        $this->historico = [];
        $this->consultas = [];
    }

    public function adicionarHistorico($descricao) {
        $this->historico[] = $descricao;
    }

    public function adicionarConsulta($data, $descricao) {
        $this->consultas[] = ["data" => $data, "descricao" => $descricao];
    }

    public function getNome() {
        return $this->nome;
    }

    public function setNome($nome) {
        $this->nome = $nome;
    }

    public function getIdade() {
        return $this->idade;
    }

    public function setIdade($idade) {
        $this->idade = $idade;
    }

    public function getSexo() {
        return $this->sexo;
    }

    public function setSexo($sexo) {
        $this->sexo = $sexo;
    }

    public function getHistorico() {
        return $this->historico;
    }

    public function getConsultas() {
        return $this->consultas;
    }

    public function getMedicoResponsavel() {
        return $this->medicoResponsavel;
    }

    public function setMedicoResponsavel($medicoResponsavel) {
        $this->medicoResponsavel = $medicoResponsavel;
    }
}

/* Classe para o médico */
class Medico {
    protected $nome;
    protected $especialidade;

    public function __construct($nome, $especialidade) {
        $this->nome = $nome;
        $this->especialidade = $especialidade;
    }

    public function getNome() {
        return $this->nome;
    }

    public function setNome($nome) {
        $this->nome = $nome;
    }

    public function getEspecialidade() {
        return $this->especialidade;
    }

    public function setEspecialidade($especialidade) {
        $this->especialidade = $especialidade;
    }
}

  /* Classe do hospital*/
  class Hospital {
      protected $nome;
      protected $endereco;
      protected $pacientes;
      protected $medicos;

      public function __construct($nome, $endereco) {
          $this->nome = $nome;
          $this->endereco = $endereco;
          $this->pacientes = [];
          $this->medicos = [];
      }

    public function adicionarPaciente(Paciente $paciente, Medico $medicoResponsavel) {
        $paciente->setMedicoResponsavel($medicoResponsavel);
        $this->pacientes[] = $paciente;
    }

    public function adicionarMedico(Medico $medico) {
        $this->medicos[] = $medico;
    }

    public function listarPacientes() {
        return $this->pacientes;
    }

    public function listarMedicos() {
        return $this->medicos;
    }
    
    public function getNome() {
        return $this->nome;
    }
    
    public function getEndereco() {
        return $this->endereco;
    }
}

/* Criando um hospital */
$nomeHospital = "Hospital Regional";
$enderecoHospital = "Av. Principal, 45, Centro - Juazeiro do Norte - CE";
$hospital = new Hospital($nomeHospital, $enderecoHospital);

/* Adicionando médicos */
$medico1 = new Medico("Dr. João", "Traumatologista");
$medico2 = new Medico("Dr. Ana", "Geral");

$hospital->adicionarMedico($medico1);
$hospital->adicionarMedico($medico2);

/* Adicionando pacientes */
$paciente1 = new Paciente("Luis", 20, "Masculino");
$paciente2 = new Paciente("Carla", 29, "Feminino");

$paciente1->adicionarHistorico("Dores de cabeça, náusea e vômito");
$paciente2->adicionarHistorico("Febre alta");

$paciente1->adicionarConsulta("2024-04-10", "Dores de cabeça frequentes");
$paciente2->adicionarConsulta("2024-04-11", "Febre recorrente");

$hospital->adicionarPaciente($paciente1, $medico1);
$hospital->adicionarPaciente($paciente2, $medico2);


/* Listando os pacientes */
echo "Hospital: " . $hospital->getNome() . "\n";
echo "Endereço: " . $hospital->getEndereco() . "\n\n";
$pacientes = $hospital->listarPacientes();

echo "Pacientes:\n";
$count = count($pacientes); /* conta o número total de pacientes */
for ($i = 0; $i < $count; $i++) {
    $paciente = $pacientes[$i];
    echo "Nome: " . $paciente->getNome() . "\n";
    echo "Idade: " . $paciente->getIdade() . "\n";
    echo "Sexo: " . $paciente->getSexo() . "\n";
    echo "Histórico: ";
    $historicoCount = count($paciente->getHistorico()); /* conta o número total de registros no histórico do paciente */
    for ($j = 0; $j < $historicoCount; $j++) {
        echo $paciente->getHistorico()[$j] . ", ";
    }
    echo "\n";

    echo "Consultas: \n";
    $consultas = $paciente->getConsultas(); /* conta a lista de consultas do paciente */
    $consultasCount = count($consultas); /* conta o número total de consultas do paciente */
    for ($k = 0; $k < $consultasCount; $k++) {
        echo "- Data: " . $consultas[$k]['data'] . ", Descrição: " . $consultas[$k]['descricao'] . "\n";
    }

    $medicoResponsavel = $paciente->getMedicoResponsavel();
    echo "Médico Responsável: " . $medicoResponsavel->getNome() . ", Especialidade: " . $medicoResponsavel->getEspecialidade() . "\n\n";
}

/* Lista os médicos */
$medicos = $hospital->listarMedicos();

echo "Médicos:\n";
$medicosCount = count($medicos); /* conta o número total de médicos */
for ($m = 0; $m < $medicosCount; $m++) {
    $medico = $medicos[$m];
    echo "Nome: " . $medico->getNome() . "\n";
    echo "Especialidade: " . $medico->getEspecialidade() . "\n";
    echo "\n";
}
?>
