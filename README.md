# Tareasem5
laboratorio 5
package com.redsocial.repositorio;

import java.util.List;

import com.redsocial.entidad.Medicamento;

public interface MedicamentoRepositorio {

	public abstract int insertaMedicamento(Medicamento obj);
	public abstract List<Medicamento> listaMedicamento(String s);
	
}
