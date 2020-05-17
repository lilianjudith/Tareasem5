# Tareasem5
laboratorio 5
package com.redsocial.repositorio;

import java.util.List;

import com.redsocial.entidad.Medicamento;

public interface MedicamentoRepositorio {

	public abstract int insertaMedicamento(Medicamento obj);
	public abstract List<Medicamento> listaMedicamento(String s);
	
}


package com.redsocial.repositorio;

import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.RowMapper;
import org.springframework.stereotype.Repository;

import com.redsocial.entidad.Medicamento;

@Repository
public class MedicamentoMySqlRepositorio implements MedicamentoRepositorio {

	@Autowired
	private JdbcTemplate jdbcTemplate;
	
	@Override
	public int insertaMedicamento(Medicamento obj) {
		String sql = "insert into medicamento values(null,?,?,?)";
		Object[] val = {obj.getNombre(), obj.getPrecio(), obj.getStock()};
		return jdbcTemplate.update(sql, val);
	}

	@Override
	public List<Medicamento> listaMedicamento(String s) {
		String sql ="select * from medicamento where nombre like ?";
		Object[] val = { s+"%" };
		
		List<Medicamento> lista =  jdbcTemplate.query(sql, val, new RowMapper<Medicamento>() {
			@Override
			public Medicamento mapRow(ResultSet rs, int rowNum) throws SQLException {
				Medicamento obj = new Medicamento();
				obj.setId(rs.getInt(1));
				obj.setNombre(rs.getString(2));
				obj.setPrecio(rs.getDouble(3));
				obj.setStock(rs.getInt(4));

				return obj;
			}
			
		});
		
		return lista;
	}

}
