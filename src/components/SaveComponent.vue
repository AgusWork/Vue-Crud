<template>
	<div class="form-container">
		<form @submit.prevent="sendForm" class="form">
			<h2 class="form-title">{{ isEditing ? "Editar Producto" : "Agregar Producto" }}</h2>
			<div class="input-group">
				<label for="name" class="label">Nombre</label>
				<input
					v-model="product.name"
					type="text"
					id="name"
					class="input-field"
					placeholder=" "
				/>
			</div>
			<div class="input-group">
				<label for="price" class="label">Precio</label>
				<input
					v-model="product.value"
					type="number"
					id="price"
					class="input-field"
					placeholder=" "
				/>
			</div>
			<button type="submit" class="submit-btn">
				{{ isEditing ? "Editar" : "Enviar" }}
			</button>
		</form>
	</div>
</template>

<style scoped>
.form-container {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 20px;
}

.form {
	background: #ffffff;
	border-radius: 15px;
	padding: 25px;
	width: 100%;
	max-width: 400px;
	box-shadow: 0 6px 20px rgba(0, 0, 0, 0.08);
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
}

.form-title {
	font-family: "Poppins", sans-serif;
	font-size: 1.6rem;
	color: #2c3e50;
	margin-bottom: 20px;
	text-align: center;
}

.input-group {
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
	position: relative;
	margin-bottom: 20px;
}

.label {
	font-family: "Roboto", sans-serif;
	font-size: 0.9rem;
	color: #7f8c8d;
	position: absolute;
	left: 15px;
	top:12px;
	pointer-events: none;
	transition: all 0.7s ease;
}
.input-field:focus {
	border-color: #3498db;
}

.input-field {
	width: 100%;
	padding: 10px;
	border: 2px solid #ecf0f1;
	border-radius: 8px;
	font-size: 1rem;
	color: #34495e;
	outline: none;
	transition: border-color 0.3s ease;
}

.input-group:has(.input-field:focus) .label,
.input-group:has(.input-field:not(:placeholder-shown)) .label {
    top: -10px;
    background: #fff;
    padding: 0 5px;
}

.submit-btn {
	width: 100%;
	padding: 10px;
	background: #3498db;
	border: none;
	border-radius: 8px;
	color: white;
	font-family: "Poppins", sans-serif;
	font-size: 1rem;
	cursor: pointer;
	transition: background 0.2s ease;
}

.submit-btn:hover {
	background: #2980b9;
}
</style>

<script>
export default {
	name: "SaveComponent",
	props: {
		products: String,
		productEdit: String,
	},
	data() {
		return {
			product: {
				name: "",
				value: "",
				id: 1,
			},
			isEditing: false,
		};
	},
	watch: {
		productEdit: {
			handler(newProduct) {
				if (newProduct && Object.keys(newProduct).length > 0) {
					this.product = { ...newProduct };
					this.isEditing = true;
				} else {
					this.resetForm();
				}
			},
			immediate: true,
		},
	},
	methods: {
		sendForm(e) {
			e.preventDefault();

			if (this.isEditing) {
				this.$emit("productUpdate", { ...this.product });
			} else {
				this.$emit("productInsert", { ...this.product });
			}

			this.resetForm();
		},
		resetForm() {
			this.product = { name: "", value: "", id: null };
			this.isEditing = false;
		},
	},
};
</script>
